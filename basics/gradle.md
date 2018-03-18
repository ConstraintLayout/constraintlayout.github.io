---
layout: content
title: Gradle Integration
author: wolfram
as_version: 3.0
cl_version: 1.0.2 or 1.1.0-beta5
order: 6
---

### Top level build configuration
You can add ConstraintLayout as you do with other dependencies: By adding it to your gradle `build.xml` file.

Since ConstaintLayout is part of the Support Library family provided by Google, you have to use the [Google Maven repository](https://developer.android.com/studio/build/dependencies.html#google-maven).

Most likely your project is using other parts of the Support Library family anyway, but to be sure, here's how to configure your top level build file to use the Google repository:

```gradle
buildscript {
  repositories {
    google()
    jcenter()
  }

  dependencies {
    classpath 'com.android.tools.build:gradle:3.0.1'
  }
}

allprojects {
  repositories {
    google()
    jcenter()
  }
}
```


### Module specific configuration
With this configuration in place, you simply add the version of ConstraintLayout you want to the module specific gradle file (usually within the `app` module):

```gradle
dependencies {
  // other libs...
  implementation 'com.android.support.constraint:constraint-layout:1.1.0-beta5'
  // other libs...
}
```


### Versions
Currently there are two versions available:
* 1.0.2 - The stable version of the 1.0 release
* 1.1.0-beta5 - The beta version of the upcoming 1.1 release

All versions are listed on Google's [maven repository](https://dl.google.com/dl/android/maven2/com/android/support/constraint/group-index.xml).

Features of the 1.1 branch that are missing in the 1.0 release:
* [Barriers](barriers.html)
* [Placeholders](https://developer.android.com/reference/android/support/constraint/Placeholder.html)
* [Groups](https://developer.android.com/reference/android/support/constraint/Group.html)
* [Circular positioning](https://developer.android.com/reference/android/support/constraint/ConstraintLayout.html#CircularPositioning)
* Percent dimensions


### Android Studio's Layout Editor
Newer features of the ConstraintLayout are best supported in newer versions of Android Studio. While the 3.0.x versions are stable, they might not support all features of the latest betas. On the other hand the 3.1 and 3.2 versions are in active development. They are bound to contain bugs and might not properly support all of the older features.

If you use XML anyway, the specific version of Android Studio is of less importance.



