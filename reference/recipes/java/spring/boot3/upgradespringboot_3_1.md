# Migrate to Spring Boot 3.1

**org.openrewrite.java.spring.boot3.UpgradeSpringBoot\_3\_1**

_Migrate applications to the latest Spring Boot 3.1 release. This recipe will modify an application's build files, make changes to deprecated/preferred APIs, and migrate configuration settings that have changes between versions. This recipe will also chain additional framework migrations (Spring Framework, Spring Data, etc) that are required as part of the migration to Spring Boot 3.0._

### Tags

* spring
* boot

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-spring/blob/main/src/main/resources/META-INF/rewrite/spring-boot-31.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-spring/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-spring/5.15.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-spring
* version: 5.15.0

{% hint style="info" %}
This recipe is composed of more than one recipe. If you want to customize the set of recipes this is composed of, you can find and copy the GitHub source for the recipe from the link above.
{% endhint %}
## Data Tables

### Source files that had results
**org.openrewrite.table.SourcesFileResults**

_Source files that were modified by the recipe run._

| Column Name | Description |
| ----------- | ----------- |
| Source path before the run | The source path of the file before the run. |
| Source path after the run | A recipe may modify the source path. This is the path after the run. |
| Parent of the recipe that made changes | In a hierarchical recipe, the parent of the recipe that made a change. Empty if this is the root of a hierarchy or if the recipe is not hierarchical at all. |
| Recipe that made changes | The specific recipe that made a change. |
| Estimated time saving | An estimated effort that a developer to fix manually instead of using this recipe, in unit of seconds. |
| Cycle | The recipe cycle in which the change was made. |

### Source files that errored on a recipe
**org.openrewrite.table.SourcesFileErrors**

_The details of all errors produced by a recipe run._

| Column Name | Description |
| ----------- | ----------- |
| Source path | The file that failed to parse. |
| Recipe that made changes | The specific recipe that made a change. |
| Stack trace | The stack trace of the failure. |

### Recipe performance
**org.openrewrite.table.RecipeRunStats**

_Statistics used in analyzing the performance of recipes._

| Column Name | Description |
| ----------- | ----------- |
| The recipe | The recipe whose stats are being measured both individually and cumulatively. |
| Source file count | The number of source files the recipe ran over. |
| Source file changed count | The number of source files which were changed in the recipe run. Includes files created, deleted, and edited. |
| Cumulative scanning time | The total time spent across the scanning phase of this recipe. |
| 99th percentile scanning time | 99 out of 100 scans completed in this amount of time. |
| Max scanning time | The max time scanning any one source file. |
| Cumulative edit time | The total time spent across the editing phase of this recipe. |
| 99th percentile edit time | 99 out of 100 edits completed in this amount of time. |
| Max edit time | The max time editing any one source file. |


## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-spring:5.15.0` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.16.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_1")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-spring:5.15.0")
}
```
{% endcode %}
2. Run `gradle rewriteRun` to run the recipe.
{% endtab %}

{% tab title="Gradle init script" %}
1. Create a file named `init.gradle` in the root of your project.
{% code title="init.gradle" %}
```groovy
initscript {
    repositories {
        maven { url "https://plugins.gradle.org/m2" }
    }
    dependencies { classpath("org.openrewrite:plugin:6.16.4") }
}
rootProject {
    plugins.apply(org.openrewrite.gradle.RewritePlugin)
    dependencies {
        rewrite("org.openrewrite.recipe:rewrite-spring:5.15.0")
    }
    rewrite {
        activeRecipe("org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_1")
    }
    afterEvaluate {
        if (repositories.isEmpty()) {
            repositories {
                mavenCentral()
            }
        }
    }
}
```
{% endcode %}
2. Run `gradle --init-script init.gradle rewriteRun` to run the recipe.
{% endtab %}
{% tab title="Maven POM" %}
1. Add the following to your `pom.xml` file:
{% code title="pom.xml" %}
```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>5.36.0</version>
        <configuration>
          <exportDatatables>true</exportDatatables>
          <activeRecipes>
            <recipe>org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_1</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-spring</artifactId>
            <version>5.15.0</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
2. Run `mvn rewrite:run` to run the recipe.
{% endtab %}

{% tab title="Maven Command Line" %}

You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

{% code title="shell" overflow="wrap" %}
```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-spring:RELEASE -Drewrite.activeRecipes=org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_1 -Drewrite.exportDatatables=true
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe UpgradeSpringBoot_3_1
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Migrate to Spring Boot 3.0](../../../java/spring/boot3/upgradespringboot_3_0.md)
* [Upgrade Gradle or Maven dependency versions](../../../java/dependencies/upgradedependencyversion.md)
  * groupId: `org.springframework.boot`
  * artifactId: `*`
  * newVersion: `3.1.x`
  * overrideManagedVersion: `false`
* [Upgrade Maven parent project version](../../../maven/upgradeparentversion.md)
  * groupId: `org.springframework.boot`
  * artifactId: `spring-boot-starter-parent`
  * newVersion: `3.1.x`
* [Update a Gradle plugin by id](../../../gradle/plugins/upgradepluginversion.md)
  * pluginIdPattern: `org.springframework.boot`
  * newVersion: `3.1.x`
* [Migrate to Spring Security 6.1](../../../java/spring/security6/upgradespringsecurity_6_1.md)
* [Migrate Spring Boot properties to 3.1](../../../java/spring/boot3/springbootproperties_3_1.md)
* [Migrate to Hibernate 6.2.x](../../../hibernate/migratetohibernate62.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_1
displayName: Migrate to Spring Boot 3.1
description: Migrate applications to the latest Spring Boot 3.1 release. This recipe will modify an application's build files, make changes to deprecated/preferred APIs, and migrate configuration settings that have changes between versions. This recipe will also chain additional framework migrations (Spring Framework, Spring Data, etc) that are required as part of the migration to Spring Boot 3.0.

tags:
  - spring
  - boot
recipeList:
  - org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_0
  - org.openrewrite.java.dependencies.UpgradeDependencyVersion:
      groupId: org.springframework.boot
      artifactId: *
      newVersion: 3.1.x
      overrideManagedVersion: false
  - org.openrewrite.maven.UpgradeParentVersion:
      groupId: org.springframework.boot
      artifactId: spring-boot-starter-parent
      newVersion: 3.1.x
  - org.openrewrite.gradle.plugins.UpgradePluginVersion:
      pluginIdPattern: org.springframework.boot
      newVersion: 3.1.x
  - org.openrewrite.java.spring.security6.UpgradeSpringSecurity_6_1
  - org.openrewrite.java.spring.boot3.SpringBootProperties_3_1
  - org.openrewrite.hibernate.MigrateToHibernate62

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_1)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.

## Contributors
Tyler Van Gorder, [Knut Wannheden](mailto:knut@moderne.io), [Nick McKinney](mailto:mckinneynichoals@gmail.com), [Patrick](mailto:patway99@gmail.com), [Tim te Beek](mailto:tim@moderne.io), Chuka Obinabo, [Alex Boyko](mailto:aboyko@vmware.com), [Jonathan Schneider](mailto:jkschneider@gmail.com), Patrick Way, [Sam Snyder](mailto:sam@moderne.io), [Jonathan Schnéider](mailto:jkschneider@gmail.com), Kun Li, [traceyyoshima](mailto:tracey.yoshima@gmail.com), [Aaron Gershman](mailto:aegershman@gmail.com), [Kyle Scully](mailto:scullykns@gmail.com), [Satvika Eda](mailto:satvika164.reddy@gmail.com), [Tim te Beek](mailto:tim.te.beek@jdriven.com), [Tracey Yoshima](mailto:tracey.yoshima@gmail.com), [Greg Adams](mailto:gadams@gmail.com), [Nick McKinney](mailto:mckinneynicholas@gmail.com), Simon Zilliken, [Greg Adams](mailto:greg@moderne.io), [Kun Li](mailto:kun@moderne.io), [Shannon Pamperl](mailto:shanman190@gmail.com), Fabian Krüger, Anu Ramamoorthy, [magicwerk](mailto:magicwerk@gmail.com), [Tim te Beek](mailto:timtebeek@gmail.com), Evie Lau, [Yifeng Jin](mailto:yifeng.jyf@alibaba-inc.com), Adam Slaski, [Johannes Jank](mailto:johannes.wengert@googlemail.com), Michel Gonzalez, Aaron Gershman, ranuradh, Daryl Robbins, nbruno, Sandeep Nagaraj, [Michael Keppler](mailto:bananeweizen@gmx.de), [Simon Verhoeven](mailto:verhoeven.simon@gmail.com), [BoykoAlex](mailto:aboyko@pivotal.io), John Burns, [Sofia Britto Schwartz](mailto:sofia.b.schwartz@gmail.com), [gideon-sunbit](mailto:gideon.pertzov@sunbit.com), Aakarshit Uppal, [Amitoj Duggal](mailto:amitojduggal@gmail.com), eocantu, Josh Soref, [Scott Jungling](mailto:scott.jungling@gmail.com), Peter Puškár, [Joan Viladrosa](mailto:joan@moderne.io), [Mike Solomon](mailto:mikesol@hey.com)
