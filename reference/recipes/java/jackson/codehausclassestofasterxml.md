# Migrate classes from Jackson Codehaus (legacy) to Jackson FasterXML

**org.openrewrite.java.jackson.CodehausClassesToFasterXML**

_In Jackson 2, the package and dependency coordinates moved from Codehaus to FasterXML._

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-jackson/blob/main/src/main/resources/META-INF/rewrite/codehaus-to-fasterxml.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-jackson/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-jackson/0.4.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-jackson
* version: 0.4.1

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

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-jackson:0.4.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.16.4")
}

rewrite {
    activeRecipe("org.openrewrite.java.jackson.CodehausClassesToFasterXML")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-jackson:0.4.1")
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
        rewrite("org.openrewrite.recipe:rewrite-jackson:0.4.1")
    }
    rewrite {
        activeRecipe("org.openrewrite.java.jackson.CodehausClassesToFasterXML")
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
            <recipe>org.openrewrite.java.jackson.CodehausClassesToFasterXML</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-jackson</artifactId>
            <version>0.4.1</version>
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
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-jackson:RELEASE -Drewrite.activeRecipes=org.openrewrite.java.jackson.CodehausClassesToFasterXML -Drewrite.exportDatatables=true
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe CodehausClassesToFasterXML
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Migrate to Jackson `@JsonInclude`](../../java/jackson/codehaus/jsonincludeannotation.md)
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.codehaus.jackson.map.JsonSerializer`
  * newFullyQualifiedTypeName: `com.fasterxml.jackson.databind.JsonSerializer`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.codehaus.jackson.map.annotate.JsonSerialize$Inclusion`
  * newFullyQualifiedTypeName: `com.fasterxml.jackson.annotation.JsonInclude$Include`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.codehaus.jackson.map.annotate.JsonSerialize`
  * newFullyQualifiedTypeName: `com.fasterxml.jackson.databind.annotation.JsonSerialize`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.codehaus.jackson.map.ObjectMapper`
  * newFullyQualifiedTypeName: `com.fasterxml.jackson.databind.ObjectMapper`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.codehaus.jackson.map.SerializationConfig$Feature`
  * newFullyQualifiedTypeName: `com.fasterxml.jackson.databind.SerializationFeature`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `org.codehaus.jackson.map.DeserializationConfig$Feature`
  * newFullyQualifiedTypeName: `com.fasterxml.jackson.databind.DeserializationFeature`
* [Rename package name](../../java/changepackage.md)
  * oldPackageName: `org.codehaus.jackson.annotate`
  * newPackageName: `com.fasterxml.jackson.annotation`
  * recursive: `true`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.jackson.CodehausClassesToFasterXML
displayName: Migrate classes from Jackson Codehaus (legacy) to Jackson FasterXML
description: In Jackson 2, the package and dependency coordinates moved from Codehaus to FasterXML.

recipeList:
  - org.openrewrite.java.jackson.codehaus.JsonIncludeAnnotation
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.codehaus.jackson.map.JsonSerializer
      newFullyQualifiedTypeName: com.fasterxml.jackson.databind.JsonSerializer
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.codehaus.jackson.map.annotate.JsonSerialize$Inclusion
      newFullyQualifiedTypeName: com.fasterxml.jackson.annotation.JsonInclude$Include
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.codehaus.jackson.map.annotate.JsonSerialize
      newFullyQualifiedTypeName: com.fasterxml.jackson.databind.annotation.JsonSerialize
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.codehaus.jackson.map.ObjectMapper
      newFullyQualifiedTypeName: com.fasterxml.jackson.databind.ObjectMapper
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.codehaus.jackson.map.SerializationConfig$Feature
      newFullyQualifiedTypeName: com.fasterxml.jackson.databind.SerializationFeature
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: org.codehaus.jackson.map.DeserializationConfig$Feature
      newFullyQualifiedTypeName: com.fasterxml.jackson.databind.DeserializationFeature
  - org.openrewrite.java.ChangePackage:
      oldPackageName: org.codehaus.jackson.annotate
      newPackageName: com.fasterxml.jackson.annotation
      recursive: true

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.jackson.CodehausClassesToFasterXML)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.

## Contributors
[Tim te Beek](mailto:tim@moderne.io)
