# Remediate vulnerabilities from the OWASP Top Ten

**org.openrewrite.java.security.OwaspTopTen**

_[OWASP](https://owasp.org) publishes a list of the most impactful common security vulnerabilities. These recipes identify and remediate vulnerabilities from the OWASP Top Ten._

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-java-security/blob/main/src/main/resources/META-INF/rewrite/owasp.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-java-security/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-java-security/2.11.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-java-security
* version: 2.11.0

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

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-java-security:2.11.0` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.16.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.security.OwaspTopTen")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-java-security:2.11.0")
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
        rewrite("org.openrewrite.recipe:rewrite-java-security:2.11.0")
    }
    rewrite {
        activeRecipe("org.openrewrite.java.security.OwaspTopTen")
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
            <recipe>org.openrewrite.java.security.OwaspTopTen</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-java-security</artifactId>
            <version>2.11.0</version>
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
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-java-security:RELEASE -Drewrite.activeRecipes=org.openrewrite.java.security.OwaspTopTen -Drewrite.exportDatatables=true
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe OwaspTopTen
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Remediate OWASP A01:2021 Broken access control](../../java/security/owaspa01.md)
* [Remediate OWASP A02:2021 Cryptographic failures](../../java/security/owaspa02.md)
* [Remediate OWASP A03:2021 Injection](../../java/security/owaspa03.md)
* [Remediate OWASP A05:2021 Security misconfiguration](../../java/security/owaspa05.md)
* [Remediate OWASP A06:2021 Vulnerable and outdated components](../../java/security/owaspa06.md)
* [Remediate OWASP A08:2021 Software and data integrity failures](../../java/security/owaspa08.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.security.OwaspTopTen
displayName: Remediate vulnerabilities from the OWASP Top Ten
description: [OWASP](https://owasp.org) publishes a list of the most impactful common security vulnerabilities. These recipes identify and remediate vulnerabilities from the OWASP Top Ten.

recipeList:
  - org.openrewrite.java.security.OwaspA01
  - org.openrewrite.java.security.OwaspA02
  - org.openrewrite.java.security.OwaspA03
  - org.openrewrite.java.security.OwaspA05
  - org.openrewrite.java.security.OwaspA06
  - org.openrewrite.java.security.OwaspA08

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.security.OwaspTopTen)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.

## Contributors
[Jonathan Leitschuh](mailto:jonathan.leitschuh@gmail.com), [Jonathan Schneider](mailto:jkschneider@gmail.com), [Patrick](mailto:patway99@gmail.com), [Sam Snyder](mailto:sam@moderne.io), [Knut Wannheden](mailto:knut@moderne.io), [Jonathan Schnéider](mailto:jkschneider@gmail.com), [Jonathan Leitschuh](mailto:Jonathan.Leitschuh@gmail.com), [Kun Li](mailto:kun@moderne.io), [Scott Jungling](mailto:scott@moderne.io), [Tim te Beek](mailto:timtebeek@gmail.com), [Kyle Scully](mailto:scullykns@gmail.com), [Simon Verhoeven](mailto:verhoeven.simon@gmail.com)
