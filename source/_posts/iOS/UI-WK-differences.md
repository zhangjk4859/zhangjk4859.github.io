---
title: Why use WKWebview
date: 2021-4-13 12:35:48
categories: 
- iOS
tags:
---

​       WK is run in a separate process so that it can draw on native Safari JavaScript optimizations,this means WK loads web pages faster than UIWeb,UIWeb uses traditional JS engines which are basic interpreters,Apple's Nitro engine uses a 4 tier compiling strategy which can execute JS 40 times faster than a traditional JS interpreter.

Nitro means Nitromethane, is a kind of fuel for car engine.

source：

- https://www.hackingwithswift.com/example-code/wkwebview/whats-the-difference-between-uiwebview-and-wkwebview#:~:text=Second%2C%20WKWebView%20is%20run%20in,much%20memory%20overhead%20for%20you
- https://zoompf.com/blog/2014/06/apples-nitro-javascript-engine-available-to-all-apps/