---
layout: content
title: Add ConstraintLayout to a project
author: seb
as_version: 3.3
cl_version: 1.1+
order: 1
---

### Top level build configuration
You can add ConstraintLayout as you do with other dependencies, by referencing it in your `build.gradle` file.

Since ConstaintLayout is part of the [AndroidX libraries](https://developer.android.com/jetpack/androidx) provided by Google, you have to make sure your build file is using the [Google Maven repository](https://developer.android.com/studio/build/dependencies.html#google-maven).

Most likely your project is using other parts of the AndroidX family anyway, but to be sure, here's how to configure your top level `build.gradle` file to use the Google repository:

```gradle
buildscript {
  repositories {
    google()
    mavenCentral()
    jcenter()
  }

  dependencies {
    classpath 'com.android.tools.build:gradle:3.3.2'
  }
}

allprojects {
  repositories {
    google()
    mavenCentral()
    jcenter()
  }
}
```

### Module specific configuration
With this configuration in place, you simply add the version of ConstraintLayout you want to the module specific Gradle file (usually within the `app` module):

```gradle
dependencies {
  // other libs...
  implementation 'androidx.constraintlayout:constraintlayout:2.0.0-alpha4'
  // other libs...
}
```

### Versions
You should be using `ConstraintLayout` 1.1.x or newer - please refer to Google's [Maven repository](https://dl.google.com/dl/android/maven2/androidx/constraintlayout/group-index.xml) for the most up-to-date information. Prefer using the AndroidX versions over the older `com.android.support` artifacts as those will not receive any further updates nor bugfixes.

Version 2.0.x is where most development is happening, and while at the time of writing it's still in alpha, it's absolutely stable enough for production usage. Besides, version 2.0 also includes `MotionLayout` which is absent from 1.x.

### Android Studio's Layout Editor
Newer features of the ConstraintLayout are best supported in newer versions of Android Studio. Generally speaking, the layout editor tends to be stable even in beta and canary versions of Studio, so it may be worth using a newer version of Studio for the newer features and bugfixes.
