---
title: flutter组件
date: 2020-11-27 11:14:54
tags:
---

### sliverList

> A sliver that places multiple box children in a linear array along the main axis.
>
> Each child is forced to have the SliverConstraints.crossAxisExtent in the cross axis but determines its own main axis extent.
>
> SliverList determines its scroll offset by "dead **reckoning**" because children outside the visible part of the sliver are not materialized, which means SliverList cannot learn their main axis extent.Instead,newly materialized children are placed **adjacent** to existing children.

