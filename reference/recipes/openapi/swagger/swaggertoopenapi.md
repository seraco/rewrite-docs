# Migrate from Swagger to OpenAPI

**org.openrewrite.openapi.swagger.SwaggerToOpenAPI**

_Migrate from Swagger to OpenAPI._

### Tags

* openapi
* swagger

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-openapi/blob/main/src/main/resources/META-INF/rewrite/swagger-2.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-openapi/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-openapi/0.5.3/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-openapi
* version: 0.5.3

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

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-openapi:0.5.3` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.16.4")
}

rewrite {
    activeRecipe("org.openrewrite.openapi.swagger.SwaggerToOpenAPI")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-openapi:0.5.3")
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
        rewrite("org.openrewrite.recipe:rewrite-openapi:0.5.3")
    }
    rewrite {
        activeRecipe("org.openrewrite.openapi.swagger.SwaggerToOpenAPI")
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
            <recipe>org.openrewrite.openapi.swagger.SwaggerToOpenAPI</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-openapi</artifactId>
            <version>0.5.3</version>
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
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-openapi:RELEASE -Drewrite.activeRecipes=org.openrewrite.openapi.swagger.SwaggerToOpenAPI -Drewrite.exportDatatables=true
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe SwaggerToOpenAPI
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Change Gradle or Maven dependency](../../java/dependencies/changedependency.md)
  * oldGroupId: `io.swagger`
  * oldArtifactId: `swagger-annotations`
  * newGroupId: `io.swagger.core.v3`
  * newVersion: `2.2.x`
* [Change Gradle or Maven dependency](../../java/dependencies/changedependency.md)
  * oldGroupId: `io.swagger`
  * oldArtifactId: `swagger-core`
  * newGroupId: `io.swagger.core.v3`
  * newVersion: `2.2.x`
* [Change Gradle or Maven dependency](../../java/dependencies/changedependency.md)
  * oldGroupId: `io.swagger`
  * oldArtifactId: `swagger-models`
  * newGroupId: `io.swagger.core.v3`
  * newVersion: `2.2.x`
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `io.swagger.annotations.Tag`
  * newFullyQualifiedTypeName: `io.swagger.v3.oas.annotations.tags.Tag`
* [Migrate from @ApiOperation to @Operation](../../openapi/swagger/migrateapioperationtooperation.md)
* [Migrate from @ApiResponses to @ApiResponses](../../openapi/swagger/migrateapiresponsestoapiresponses.md)
* [Migrate from @ApiImplicitParams  to @Parameters](../../openapi/swagger/migrateapiimplicitparamstoparameters.md)
* [Migrate from @Api to @Tag](../../openapi/swagger/migrateapitotag.md)
* [Migrate from @ApiParam to @Parameter](../../openapi/swagger/migrateapiparamtoparameter.md)
* [Migrate from @ApiModelProperty to @Schema](../../openapi/swagger/migrateapimodelpropertytoschema.md)
* [Change type](../../java/changetype.md)
  * oldFullyQualifiedTypeName: `io.swagger.annotations.ApiModel`
  * newFullyQualifiedTypeName: `io.swagger.v3.oas.annotations.media.Schema`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.openapi.swagger.SwaggerToOpenAPI
displayName: Migrate from Swagger to OpenAPI
description: Migrate from Swagger to OpenAPI.
tags:
  - openapi
  - swagger
recipeList:
  - org.openrewrite.java.dependencies.ChangeDependency:
      oldGroupId: io.swagger
      oldArtifactId: swagger-annotations
      newGroupId: io.swagger.core.v3
      newVersion: 2.2.x
  - org.openrewrite.java.dependencies.ChangeDependency:
      oldGroupId: io.swagger
      oldArtifactId: swagger-core
      newGroupId: io.swagger.core.v3
      newVersion: 2.2.x
  - org.openrewrite.java.dependencies.ChangeDependency:
      oldGroupId: io.swagger
      oldArtifactId: swagger-models
      newGroupId: io.swagger.core.v3
      newVersion: 2.2.x
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.swagger.annotations.Tag
      newFullyQualifiedTypeName: io.swagger.v3.oas.annotations.tags.Tag
  - org.openrewrite.openapi.swagger.MigrateApiOperationToOperation
  - org.openrewrite.openapi.swagger.MigrateApiResponsesToApiResponses
  - org.openrewrite.openapi.swagger.MigrateApiImplicitParamsToParameters
  - org.openrewrite.openapi.swagger.MigrateApiToTag
  - org.openrewrite.openapi.swagger.MigrateApiParamToParameter
  - org.openrewrite.openapi.swagger.MigrateApiModelPropertyToSchema
  - org.openrewrite.java.ChangeType:
      oldFullyQualifiedTypeName: io.swagger.annotations.ApiModel
      newFullyQualifiedTypeName: io.swagger.v3.oas.annotations.media.Schema

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.openapi.swagger.SwaggerToOpenAPI)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.

## Contributors
[Tim te Beek](mailto:tim@moderne.io)
