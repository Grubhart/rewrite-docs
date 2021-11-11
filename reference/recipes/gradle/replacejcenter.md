# Replace JCenter with Maven Central

** org.openrewrite.gradle.ReplaceJCenter**
_The JCenter public artifact repository has shut down. This recipe updates bulid.gradle repository declarations to use Maven Central instead._

## Source

[Github](https://github.com/openrewrite/rewrite-gradle), [Issue Tracker](https://github.com/openrewrite/rewrite-gradle/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-gradle/7.16.1/jar)

* groupId: org.openrewrite
* artifactId: rewrite-gradle
* version: 7.16.1


## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite:rewrite-gradle:7.16.1 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.14.0")
}

rewrite {
    activeRecipe("org.openrewrite.gradle.ReplaceJCenter")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite:rewrite-gradle:7.16.1")
}
```
{% endcode %}
{% endtab %}

{% tab title="Maven" %}
{% code title="pom.xml" %}
```markup
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>4.16.0</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.gradle.ReplaceJCenter</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite</groupId>
            <artifactId>rewrite-gradle</artifactId>
            <version>7.16.1</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-DactiveRecipe=org.openrewrite.gradle.ReplaceJCenter`

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Remove repository](../gradle/removerepository.md)
  * repository: `jcenter`
* [Add repository](../gradle/addrepository.md)
  * repository: `mavenCentral`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.gradle.ReplaceJCenter
displayName: Replace JCenter with Maven Central
description: The JCenter public artifact repository has shut down. This recipe updates bulid.gradle repository declarations to use Maven Central instead.
recipeList:
  - org.openrewrite.gradle.RemoveRepository:
      repository: jcenter
  - org.openrewrite.gradle.AddRepository:
      repository: mavenCentral

```
{% endtab %}
{% endtabs %}
