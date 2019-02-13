---
layout: content
title: Backgrounds
author: mark
as_version: 2.4 alpha 7
cl_version: 1.0.2
---
### Backgrounds

A common pattern in Android layouts is where we need to visually group a collection of views together, and the visual indicator of that grouping is a common background which wraps those views. Normally we would achieve this by using a `ViewGroup` to which the background is applied, set its `android:layout_[width|height]="wrap_content"`, and add the views we wish to group as children. The downside of this is that nested layouts can be expensive during the layout pass, and they also make using `TransitionManager` a little harder, so current best practice is to keep layouts as flat as possible. `ConstraintLayout` allows us to do this with no nesting - keeping the background and all of the children we wish to visually group as immediate children of the `ConstraintLayout`.
  
#### Some fundamentals

There are a couple of important principles that we need to be aware of. Firstly (apart from some cases when animating) Android will draw views in the order in which they appear within the layout DOM. So if we occupy the same space with two separate views, the one which appears last in the layout DOM will be drawn on top of the one which appears first.

The second principle is concerning view IDs. A view ID is first declared in the layout by using the `+` prefix to the `id` resource type: `@+id/background`. This does not _have_ to be an attribute of the view which it identifies. In other words it is possible for a view to reference another view which appears later in the layout provided it uses the `+` prefix in the id reference. That ensures that the id will be created if it does not already exist.

These two principles are true of all Android layouts, not just `ConstraintLayout`, but they are key to understanding how this technique works.

#### Creating a background in the editor

To create a visual background for a group of views, we must first create a simple `View` object to which we apply the background colour or drawable in the `android:background` attribute (adding this before the other views will cause it to be drawn behind the others). It is worth giving this some fixed dimensions initially otherwise it will be difficult to manipulate later - we'll change these as we go. Next add the views that we wish to visually group together, and add the necessary constraints to position them correctly but do not constrain anything to the background view that we just created. Once they are in position, we can now constrain the background view to the positions of visual children (i.e. the Views which will appear to be child Views of the background View).

It is actually quite difficult to see these constraints if we do them all at once, so let's look at them side by side and focus on how we constrain the verticals of the background view (on the right) to the visual children (on the left):

![Background vertical constraints]({{ '/assets/images/cookbook/background_alignment.gif' | absolute_url  }} )

There is a really important thing to note here: When we first create the constraint, a default `android:layout_marginTop='8dp'` is applied to the background view. As a result of this, the top edge is `8dp` lower than the top edge of the view that we're constraining it to. If we consider the expected behaviour if we were to constrain the background to the parent, then this makes perfect sense. However, as we shall see very shortly, we need to properly understand how margins will affect the background view. For now we set the margin to `0dp` to get it to align to the top of the view that we're constraining it to.

Next we must apply exactly the same technique to the horizontal constraints and we can get the background view to appear as though it were a parent `ViewGroup` set to `wrap_content`:

![Background no padding]({{ '/assets/images/cookbook/background_no_padding.png' | absolute_url  }} )

That is the basic principle: draw the background view before any of its visual children, and then constrain it to the visual children at the edges of the visual group. But there is a complication: What if we want to increase the border around the visual children? We have already seen that if we were to add a margin to the background view it would actually move the top edge down making the top visual child draw slightly outside the background rather than increasing the border.

#### The box model

To understand how we can do what we need, it's worth a quick introduction to the Android box model, which is very similar to the HTML box model. Every view has a bounding box which represents the measured size and location within the layout. We can add whitespace around the view by setting either a `android:layout_margin*` or an `android:padding*` value, but margins and paddings add whitespace in subtly different ways. A margin will add space _outside_ the bounding box: it will cause the position of the bounding box to change, but will not affect its measured size. Whereas a padding will add space _inside_ the bounding box: it will not affect the position of the bounding box, but will cause its measured size to change.

When we constrain the background view to another view, then it is actually constrained to the bounding box of that other view. If we were to apply a margin to that other view, then it would move the bounding box and so the background will move with it. However if we apply a padding to the other view then the position of the bounding box will not change (so the background view will not move) but whitespace will be added inside the bounding box. 

If we apply margins to all of the views to which the background view is constrained, then this offsets the background from the edge of the parent; and if we also apply padding to those same views then we can also create an offset of those views from the edge of the background, thus giving a border around them:

![Background padding]({{ '/assets/images/cookbook/background_padding.png' | absolute_url  }} )
  
### The XML

Although there are some concepts that we need to understand in order to achieve this effect, the XML is actually quite straightforward once we understand them:

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
    android:padding="8dp"
    app:layout_constraintEnd_toEndOf="@+id/textView1"
    app:layout_constraintStart_toStartOf="@+id/textView1"
    app:layout_constraintTop_toBottomOf="@+id/textView1"
    tools:text="TextView" />

  <TextView
    android:id="@+id/textView3"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:padding="8dp"
    app:layout_constraintEnd_toEndOf="@+id/textView1"
    app:layout_constraintStart_toStartOf="@+id/textView1"
    app:layout_constraintTop_toBottomOf="@+id/textView2"
    tools:text="TextView" />
</android.support.constraint.ConstraintLayout>
```

The `background` appears earlier in the XML than the three `TextView` instances which will be its visual children to ensure that they are drawn on top of the background. The `background` is constrained to the `top`, `start`, and `end` edges of `textView1`; and the `bottom` edge of `textView3`. The margins of `textView1` & `textView3` control the space between the parent edges and `background`; and the paddings control the space between the edges of `background` and where the text in the `TextView` instances is drawn.
