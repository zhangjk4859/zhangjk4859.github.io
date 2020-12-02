---
title: 什么是bitCode
date: 2020-12-02 07:45:52
tags:
---

The process of compiling consists of three different steps:

1.The compilier front-end converts the source code into some kind of intermediate representation.

2.The optimizer performs a sequence of optimizing transformations on the IR to render it smaller and more performant:redundant code is removed,results are pretaculated,code is inlined, etc.This crucial step of the compilation process makes use of IR,rather than cource code or machine code,because it can more easily be interreted by the optimizer.

3. The compilier back-end generates machine code based on the optimized IR. 

When we are talking about bitcode,we are actually talking about the IR used by the Clang Compilier.

![image](https://www.guardsquare.com/files/media/guardsquare2017/Compiling-with-bitcode-enabled.png)

With the bitcode embedded in the executable,Apple is able to recompile applications without interacting with the developer.This has a lot of advantages. 

source:https://www.guardsquare.com/en/blog/enable-bitcode