---
title: flutter App optimization
date: 2021-3-31 10:50:49
categories: 
- flutter
tags:
---

- avoid costly work in build() since build() can be invoked frequently when ancestor Widgets rebuild

- avoid calling setState() high up in the tree

- Use the lazy methods, with callbacks,when building large grids or lists, that way only the visible portion of the screen is built at startup time

- avoid invoke saveLayer(),including

  - opacity widget
  - shaderMask
  - colorFilter
  - Clip
  - Text
  - addition:Clipping doesn't call saveLayer() but is still costly

  Ways to avoid calls to saveLayer():

  - To implement fading in an image, consider using the FadeInImage
  - using the border Radius property instead of applying a clipping rectangle

- build and display frames in 16ms
- build  subtree widget once and pass it as a child to the AnimatedBuilder
- pre-clip image before animating it
- avoid using constructors with a concrete List of children if most of the children are not visible on  screen

source:https://flutter.dev/docs/perf/rendering/best-practices