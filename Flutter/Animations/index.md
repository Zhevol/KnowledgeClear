---
layout: page
title: Flutter 的动画
permalink: /animations/
---

* TOC Placeholder
{:toc}

优秀的动画设计使用户界面感觉更直观，让精美的应用程序有了更灵动的外观和感觉，同时还提升了用户体验。 Flutter 的动画支持能够轻松实现各种各样的动画类型。许多控件，特别是[Material Design 控件](https://flutter.io/widgets/material/)，在其设计规范中就定义了标准的运动效果，但也可以自定义这些效果。

以下资源是开始学习 Flutter 动画框架的好地方。文档中一步一步的展示了如何编写动画的代码。 {% comment %} 更多关于如何实现通用设计样式的文档，例如共享元素转变和基于物理的动画。如果你有一个具体的需求，请[提交一个 issue ](https://github.com/flutter/flutter/issues)。 {% endcomment %}

* [教程： Flutter 的动画](/tutorials/animation/)<br>
解释了Flutter动画包中的（控制器、动画、曲线、监听器、建造者）基本的类，它会引导你
Explains the fundamental classes in the Flutter animation package
(controllers, Animatable, curves, listeners, builders),
as it guides you through a progression of tween animations using
different aspects of the animation APIs.

* [Zero to One with Flutter, part
1](https://medium.com/dartlang/zero-to-one-with-flutter-43b13fd7b354) and [part
2](https://medium.com/dartlang/zero-to-one-with-flutter-part-two-5aa2f06655cb)<br>
Medium articles showing how to create an animated chart using tweening.

* [Building Beautiful UIs with
Flutter](https://codelabs.developers.google.com/codelabs/flutter/index.html#0)<br>
Codelab demonstrating how to build a simple chat app. [Step 7 (Animate
your app)](https://codelabs.developers.google.com/codelabs/flutter/index.html#6)
shows how to animate the new message&mdash;sliding it from the input area up
to the message list.

## Animation types

Animations fall into one of two categories: tween- or physics-based.
The following sections explain what these terms mean, and points you to
resources where you can learn more. In some cases,
the best documentation we currently have is example code in the
Flutter gallery.

### Tween animation

Short for _in-betweening_. In a tween animation, the beginning
and ending points are defined, as well as a timeline, and a curve
that defines the timing and speed of the transition.
The framework calculates how to transition from the beginning point
to the end point.

The documents listed above, such as the [animations
tutorial](/tutorials/animation/) aren't about tweening,
specifically, but they use tweens in their examples.

### Physics-based animation

In physics-based animation, motion is modeled to resemble real-world
behavior. When you toss a ball, for example, where and when
it lands depends on how fast it was tossed, how heavy it is, and how
far off the ground. Similarly, dropping a ball attached to a spring falls
(and bounces) differently than dropping a ball attached to a string.

* [Flutter Gallery](https://github.com/flutter/flutter/tree/master/examples/flutter_gallery)<br>
Under **Material Components**, the
[Grid](https://github.com/flutter/flutter/blob/master/examples/flutter_gallery/lib/demo/material/grid_list_demo.dart) example
demonstrates a fling animation. Select one of the images from
the grid and zoom in. You can pan the image with flinging or dragging
gestures.

* Also see the API documentation for
[AnimationController.animateWith](https://docs.flutter.io/flutter/animation/AnimationController/animateWith.html) and
[SpringSimulation](https://docs.flutter.io/flutter/physics/SpringSimulation-class.html).

## Common animation patterns

Most UX or motion designers find that certain animation patterns are
used repeatedly when designing a UI. This section lists some of the commonly
used animation patterns, and tells you where you can learn more.

### Animated list or grid
This pattern involves animating the addition or removal of elements from a
list or grid.

* [AnimatedList example](/catalog/samples/animated-list/)<br>
This demo, from the [Sample App Catalog](/catalog/samples), shows how to
animate adding an element to a list, or removing a selected element.
The internal Dart list is synced as the user modifies the list using
the plus (+) and minus (-) buttons.

### Shared element transition

In this pattern, the user selects an element&mdash;often an
image&mdash;from the page, and the UI animates the selected element
to a new page with more detail. In Flutter, you can easily implement
shared element transitions between routes (pages) using the Hero widget.

* [Hero Animations](/animations/hero-animations/)
How to create two styles of Hero animations:
  * The hero flies from one page to another while changing position
    and size.
  * The hero's boundary changes shape, from a circle to a square,
    as its flies from one page to another.

* [Flutter Gallery](https://github.com/flutter/flutter/tree/master/examples/flutter_gallery)<br>
You can build the Gallery app yourself, or download it from the Play Store.
The [Shrine](https://github.com/flutter/flutter/blob/master/examples/flutter_gallery/lib/demo/shrine_demo.dart)
demo includes an example of a Hero animation.

* Also see the API documentation for the
[Hero,](https://docs.flutter.io/flutter/widgets/Hero-class.html)
[Navigator,](https://docs.flutter.io/flutter/widgets/Navigator-class.html) and
[PageRoute](https://docs.flutter.io/flutter/widgets/PageRoute-class.html)
classes.

### Staggered animation

Animations that are broken into smaller motions, where some of the motion is delayed.
The smaller animations may be sequential, or may partially or completely overlap.

* [Staggered Animations](/animations/staggered-animations/) <img src="/images/ic_new_releases_black_24px.svg" alt="this doc is new!"> NEW<br>

## Other resources

Learn more about Flutter animations at the following links:

* [Animations: Technical Overview](/animations/overview.html)<br>
A look at some of the major classes in the animations library,
and Flutter's animation architecture.

* [Animation and Motion Widgets](/widgets/animation/)<br>
A catalog of some of the animation widgets provided in the Flutter APIs.

{% comment %}
Until the landing page for the animation library is reworked, leave this
link out.
* The [animation
library](https://docs.flutter.io/flutter/animation/animation-library.html)
in the [Flutter API documentation](https://docs.flutter.io/)<br>
The animation API for the Flutter framework.
{% endcomment %}

<hr>

If there is specific animation documentation you'd like to see, please
[file an issue](https://github.com/flutter/flutter/issues).

