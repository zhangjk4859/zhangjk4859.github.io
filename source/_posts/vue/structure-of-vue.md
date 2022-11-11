---
title: Structure of Vue
date: 2021-12-24 19:15:35
categories: 
- vue
tags:
---

[Introduction to Vue.js](https://www.youtube.com/watch?v=MmgswF5GFf8)

[What is Vue Router](https://www.youtube.com/watch?v=nKg_p89Hzos)

[Learn vuex in 15 minutes](https://www.youtube.com/watch?v=oxUyIzDbZts)

[Reactivity in Depth](https://vuejs.org/v2/guide/reactivity.html)

![image](https://miro.medium.com/max/1400/1*ypvWdsbWb18Hl-xq016ytA.png)

Tips:

- In a traditional app that is not using client-side routing,the browser is essentially going out and fetching the different content that we need from those different urls
- With a Single Page Application,we're really only looking at one page,the **index.html**,and as we click around in it, we're adjusting which view we're seeing of that app, hence we call it a single page application, because all of these pages come from that one **index.html** page.
-  【router-view】  is a placeholder replaced by route's component
- In client-side routing,when navigation happens, Vue with the help of Vue router compares and renders the differences without ever having to reload the page

![image](https://static.javatpoint.com/tutorial/vue-js/images/vue-js-reactivity-system.png)

![image](https://miro.medium.com/max/1400/1*QN4Gf4ZCJNi4-C60Q4L5SQ.png)

![image](https://miro.medium.com/max/1400/1*xr6nDJ7gy4glRZe_lAfHrQ.png)

![image](https://codingexplained.com/wp-content/uploads/2017/04/Vue-instance-lifecycle-Page-1.png)

### Q:What is One-Way Data Flow

**A:** All props form a one-way-down binding between the child property and the parent one:when the parent property updates,it will flow down to the child,but not the other way around.This prevents child components from accidentally mutating the parent's state, which can make your app's data flow harder to understand.

Ref:https://vuejs.org/v2/guide/components-props.html#One-Way-Data-Flow

### Q:What is Computed Property

**A:** In-template expressions are very convenient, but they are meant for simple operations. Putting too much logic in your templates can make them bloated and hard to maintain. For example:

```
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```

At this point, the template is no longer simple and declarative. You have to look at it for a second before realizing that it displays `message` in reverse. The problem is made worse when you want to include the reversed message in your template more than once.That’s why for any complex logic, you should use a **computed property**.Computed property is much more like a function,but what's the difference? For the end result, the two approaches are indeed exactly the same. However, the difference is that **computed properties are cached based on their reactive dependencies.** A computed property will only re-evaluate when some of its reactive dependencies have changed. This means as long as `message` has not changed, multiple access to the `reversedMessage` computed property will immediately return the previously computed result without having to run the function again.In comparison, a method invocation will **always** run the function whenever a re-render happens.

Ref:https://vuejs.org/v2/guide/computed.html#Computed-vs-Watched-Property



## The Route Object

A **route object** represents the state of the current active route. It contains parsed information of the current URL and the **route records** matched by the URL.The route object is immutable.Every successful navigation will result in [a fresh route object](https://router.vuejs.org/api/#the-route-object)

![image](https://dotblogsfile.blob.core.windows.net/user/chris%20chen/a38af4ca-3e68-4115-ab56-355d92d0e792/1488768217_35567.png)







