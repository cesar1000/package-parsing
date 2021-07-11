# Package name is dropped in precompiled script with @file:Suppress() annotation

This repros a bug where using using a `@file:Suppress()` annotation at the top of a precompiled Kotlin script causes the package declaration to be dropped:

```
$ ./gradlew :build

BUILD SUCCESSFUL in 3s
13 actionable tasks: 12 executed, 1 up-to-date

$ ls /Users/cpuerta/temp/gradle_issue_16154_package_parsing/build/generated-sources/kotlin-dsl-plugins/kotlin/
MyPluginWithSuppressPlugin.kt  com/

$ cat build/kotlin-dsl/plugins-blocks/extracted/my-plugin-with-suppress.gradle.kts




plugins {
    java
}

$ cat build/kotlin-dsl/plugins-blocks/extracted/com/twitter/my-plugin.gradle.kts
package com.twitter;

plugins {
    java
}
```
