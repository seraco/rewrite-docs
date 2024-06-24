# `AssertJCharSequenceRules` Refaster recipes

**tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes**

_Refaster template recipes for `tech.picnic.errorprone.refasterrules.AssertJCharSequenceRules`. [Source](https://error-prone.picnic.tech/refasterrules/AssertJCharSequenceRules)._

## Recipe source

[GitHub](https://github.com/search?type=code&q=tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes), [Issue Tracker](https://github.com/openrewrite/rewrite-third-party/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-third-party/0.5.1/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-third-party
* version: 0.5.1

{% hint style="info" %}
This recipe is composed of more than one recipe. If you want to customize the set of recipes this is composed of, you can find and copy the GitHub source for the recipe from the link above.
{% endhint %}

## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-third-party:0.5.1` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.16.1")
}

rewrite {
    activeRecipe("tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-third-party:0.5.1")
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
    dependencies { classpath("org.openrewrite:plugin:6.16.1") }
}
rootProject {
    plugins.apply(org.openrewrite.gradle.RewritePlugin)
    dependencies {
        rewrite("org.openrewrite.recipe:rewrite-third-party:0.5.1")
    }
    rewrite {
        activeRecipe("tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes")
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
        <version>5.34.0</version>
        <configuration>
          
          <activeRecipes>
            <recipe>tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-third-party</artifactId>
            <version>0.5.1</version>
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
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-third-party:RELEASE -Drewrite.activeRecipes=tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes 
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe AssertJCharSequenceRulesRecipes
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Refaster template `AssertJCharSequenceRules.AssertThatCharSequenceIsEmpty`](../../../../tech/picnic/errorprone/refasterrules/assertjcharsequencerulesrecipes$assertthatcharsequenceisemptyrecipe.md)
* [Refaster template `AssertJCharSequenceRules.AssertThatCharSequenceIsNotEmpty`](../../../../tech/picnic/errorprone/refasterrules/assertjcharsequencerulesrecipes$assertthatcharsequenceisnotemptyrecipe.md)
* [Refaster template `AssertJCharSequenceRules.AssertThatCharSequenceHasSize`](../../../../tech/picnic/errorprone/refasterrules/assertjcharsequencerulesrecipes$assertthatcharsequencehassizerecipe.md)

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes
displayName: `AssertJCharSequenceRules` Refaster recipes
description: Refaster template recipes for `tech.picnic.errorprone.refasterrules.AssertJCharSequenceRules`. [Source](https://error-prone.picnic.tech/refasterrules/AssertJCharSequenceRules).
recipeList:
  - tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes$AssertThatCharSequenceIsEmptyRecipe
  - tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes$AssertThatCharSequenceIsNotEmptyRecipe
  - tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes$AssertThatCharSequenceHasSizeRecipe

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/tech.picnic.errorprone.refasterrules.AssertJCharSequenceRulesRecipes)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.