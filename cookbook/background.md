---
layout: content
title: Background
author: mark
as_version: 2.4 alpha 7
cl_version: 1.0.2
---
### Background

A common pattern in Android layouts is where we need to visually group a collection of views together and we and the visual indicator of that grouping is a common background which wraps those views. Normally we would achieve this by using a `ViewGroup` to which the backgroudn is applied, set its `android:layout_[width|height]="wrap_contents"`, and add the views we wish to group as children. The downside of this is that nested layouts can be expensive during the layout pass, and they also make using `TransitionManager` a little harder, so current best practice is to keep layouts as flat as possible. `ConstraintLayout` allows us to do this with no nesting - keeping the the background and all of the children we wish to visually group as immediate children of the `ConstraintLayout`.
  
#### Some fundamentals

There are a couple of important principles that we need to be aware of. Firstly (apart from some cases when animating) Android will draw views in the order in which they appear within the layout DOM. So if we occupy the same space with two separate views, the one which appears last in the layout DOM will be drawn on top of the one which appears first.

The second principle is concerning view IDs. A view ID is first declared in the layout by using the `+` prefix to the `id` resource type: `@+id/background`. This does not need to be within the view which it identifies. In other words it is possible for a view to reference another view which appears later in the layout DOM provided it uses the `+` prefix in the id reference. That ensures that the id will be created if it does not already exist.

These two principles are true of all Android layouts, not just `ConstraintLayout`, but they are key to understanding how this technique works.

#### Creating a background in the editor

To create a visual background for a group of views, we must first create a simple `View` object to which we apply the background colour or drawable in the `android:background` attribute (adding this before the other views will cause it to appear first in the layout DOM). 
  
### The XML

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout 
  xmlns:android="http://schemas.android.com/apk/res/android"
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