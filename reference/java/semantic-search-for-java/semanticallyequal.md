---
description: Determine semantic equality between two abstract syntax trees.
---

# SemanticallyEqual

{% hint style="info" %}
**Semantic Equality:** Two pieces of code are semantically equal if they produce the same behavior.
{% endhint %}

`SemanticallyEqual` recursively checks the equality of each element of two abstract syntax trees \(ASTs\) to determine if the two trees are semantically equal. This is necessary because ASTs are so frequently recreated that merely comparing the IDs of two ASTs is ineffective.

## Java Definition

{% hint style="warning" %}
`SemanticallyEqual` has only been implemented for annotations for now. If you would like to see more functionality, join the [OpenRewrite Slack](https://join.slack.com/t/rewriteoss/shared_invite/zt-kpz9t4hw-oWFbOMy~Kxta28qr2uqSFg) and tell us more about it! We are also accepting pull requests at the [OpenRewrite Github](https://github.com/openrewrite/rewrite). 
{% endhint %}

```java
J.Annotation annot;
J.Annotation otherAnnot;

Boolean isEqual = SemanticallyEqual.areEqual(annot, otherAnnot);
```

## Example

This example is in Kotlin. It demonstrates how both the annotation type and arguments must be checked for equality.

While the IDs of the first two `@Tag` annotations are different, `SemanticallyEqual` compares uses the annotation type and the arguments to determine that they are indeed semantically equal. `@Tag(SlowTests.class)` is not semantically equal to either because its argument is different.

```kotlin
val cu = jp.parse(
    """
        @Tag(FastTests.class)
        @Tag(FastTests.class)
        @Tag(SlowTests.class)
        class A {}
    """,
    """
        @interface Tags {
            Tag[] value();
        }
    """,
    """
        @java.lang.annotation.Repeatable(Tags.class)
        @interface Tag {
            Class value();
        }
    """,
    "public interface FastTests {}",
    "public interface SlowTests {}"
)

val fastTest = cu[0].classes[0].annotations[0]
val fastTest2 = cu[0].classes[0].annotations[1]
val slowTest = cu[0].classes[0].annotations[2]

assertThat(SemanticallyEqual.areEqual(fastTest, fastTest2)).isTrue()
assertThat(SemanticallyEqual.areEqual(fastTest, slowTest)).isFalse()
```

