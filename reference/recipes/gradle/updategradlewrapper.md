# Update Gradle wrapper

** org.openrewrite.gradle.UpdateGradleWrapper**
_Update the version of Gradle used in an existing Gradle Wrapper._

## Source

[Github](https://github.com/openrewrite/rewrite-gradle), [Issue Tracker](https://github.com/openrewrite/rewrite-gradle/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-gradle/7.22.0/jar)

* groupId: org.openrewrite
* artifactId: rewrite-gradle
* version: 7.22.0

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | version | *Optional*. The version of Gradle to use. Defaults to 7.4.2 |
| `String` | distribution | *Optional*. The distribution of Gradle to use. "bin" includes Gradle binaries. "all" includes Gradle binaries, source code, and documentation. If not specified the existing distribution type will be used. |
| `String` | distributionUrl | *Optional*. The URL to download the Gradle distribution from. Providing the distribution url overrides the "Version" and "Distribution type" parameters. This is intended to cover customized distributions of the Gradle wrapper. |


## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite:rewrite-gradle:7.22.0 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.20.0")
}

rewrite {
    activeRecipe("org.openrewrite.gradle.UpdateGradleWrapper")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite:rewrite-gradle:7.22.0")
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
        <version>4.23.0</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.gradle.UpdateGradleWrapper</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite</groupId>
            <artifactId>rewrite-gradle</artifactId>
            <version>7.22.0</version>
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

Recipes can also be activated directly from the command line by adding the argument `-DactiveRecipe=org.openrewrite.gradle.UpdateGradleWrapper`
