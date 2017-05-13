---
layout: content
title: Centring
author: mark
as_version: 2.4 alpha 7
cl_version: 1.0.2
---
### Centring

#### Centring in the parent in the editor

![Centring in the parent](../assets/images/tricks/centring_parent.gif)

#### Centring in the parent in XML

```xml
  <TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toBottomOf="parent"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"/>
```

#### Centring to the middle of a sibling in the editor

![Centring in the parent](../assets/images/tricks/centring_sibling_middle.gif)

#### Centring to the middle of a sibling in XML

```xml
  <TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toTopOf="@+id/imageView"
    app:layout_constraintBottom_toBottomOf="@+id/imageView"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"/>
```

#### Centring to the edge of a sibling in the editor

![Centring in the parent](../assets/images/tricks/centring_sibling_edge.gif)

#### Centring to the edge of a sibling in XML

```xml
  <TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:layout_constraintTop_toBottomOf="@+id/imageView"
    app:layout_constraintBottom_toBottomOf="@+id/imageView"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"/>
```