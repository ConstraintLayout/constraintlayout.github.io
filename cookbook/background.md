---
layout: content
title: Background
author: mark
as_version: 2.4 alpha 7
cl_version: 1.0.2
---
### Background

### The XML

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:background="#AAA">

  <View
    android:id="@+id/background"
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:layout_marginTop="0dp"
    android:background="#FFF"
    app:layout_constraintBottom_toBottomOf="@+id/textView3"
    app:layout_constraintEnd_toEndOf="@+id/textView1"
    app:layout_constraintStart_toStartOf="@+id/textView1"
    app:layout_constraintTop_toTopOf="@+id/textView1" />

  <TextView
    android:id="@+id/textView1"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_margin="8dp"
    android:padding="8dp"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    tools:text="TextView" />

  <TextView
    android:id="@+id/textView2"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_marginEnd="0dp"
    android:layout_marginStart="0dp"
    android:padding="8dp"
    app:layout_constraintEnd_toEndOf="@+id/textView1"
    app:layout_constraintStart_toStartOf="@+id/textView1"
    app:layout_constraintTop_toBottomOf="@+id/textView1"
    tools:text="TextView" />

  <TextView
    android:id="@+id/textView3"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_marginEnd="0dp"
    android:layout_marginStart="0dp"
    android:layout_marginTop="0dp"
    android:padding="8dp"
    app:layout_constraintEnd_toEndOf="@+id/textView1"
    app:layout_constraintStart_toStartOf="@+id/textView1"
    app:layout_constraintTop_toBottomOf="@+id/textView2"
    tools:text="TextView" />
</android.support.constraint.ConstraintLayout>
```