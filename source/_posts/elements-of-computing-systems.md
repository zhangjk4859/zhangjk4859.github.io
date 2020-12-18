---
title: elements-of-computing-systems
date: 2020-11-29 21:50:51
tags:
---

### The road Down to Hardware Land

Before any program can actually run and do something for real,it must be translated into the machine language of some target computer platform.This compilation process is sufficiently complex to be broken into several layers of abstraction,and these usually involve three translators: a compiler ,a virtual machine implementation ,and an assembler.We devote five book chapters to this trio,as follows.

​    The translation task of the *compilier* is performed in two conceptual stages:syntax analysis and code generation.First,the source text is analyzed and grouped into meaningful language contructs that can be kept in a data structure called a "parse tree".These parsing tasks,collectively knows as syntax analysis,are described in chapter 10.This sets the stages for chapter 11,which shows how the parse tree can be recursively processed to yield a program written in an intermediate language.As with Java and C#,the intermediator code generated by the Jack compilier describes a sequence of generic steps operating on a stack-based virtual machine(VM).This classical model ,as well as a VM implemetation that realizes in on an actual computer,are elaborated in chapters 7-8.Since the output of our VM implementation  is a large assembly program,we have to translate it further into binary code.Writing an assembler is a relatively simple task, taken up in chapter 6.

### Boolean Logic

Every digital device -be it a personal computer,a cellular telephone,or a network router-is based on a set of chips designed to store and process information. Although these chips come in different shapes and forms,they are all made from the same building blocks:Elementary *logic* *gates*.The gates can be physically implemented in many different material and --fabrication-- technologies,but their logical behavior,or interface,is --consistent -- across all computers.In this chapter we start out with one --primitive-- logic gate-Nand-- and build all the other logic gates from it.The result is a rather standard set of gates, which will be later used to construct our computer's processing and storage chips.This will be done in chapters 2 and 3,respectively.

##### Canonical Representation 

As it turns out,every Boolean function can be expressed using at least one Boolean expression called the canonical representation. Starting with the function's truth table,we focus on all the rows in which the function has value 1.For each such row,we construct a term created by And-ing together literals that fix the value of all the row's inputs.For example,let us focus on the third row in figure 1.1,where the function's value is 1.Since the variable values in this row are x=0,y=1,z=0,we construct the term xy-z- and xyz- for rows 5 and 7.Now,if we Or-together all these terms,we get a Boolean expression that is equivalent to the given truth table.Thus the canonical representation of the boolean function shown in figure 1.1 is f(x,y,z)= x-yz- + xy-z- + xyz-.This contruction leads to an important conclusion:Every Boolean function ,no matter how complex,can be expressed using three Boolean operators only:And, Or and Not. 



#### Two-Input Boolean Function 

An inspection of figure 1.1 reveals that the number of Boolean functions that can be defined over n binary variables is 2^2^n.For example,the sixteen Boolean functions spanned by two variables are listed in figure 1.2.These functions were constructed systematically,by enumerating all the possible 4-wise combinations of binary values in the four right columns.Each function has a conventional name that seeks to describe its underlying operation.Here are some examples: The name of the Nor function is shorthand for Not-Or:Take the Or of x and y,then --negate-- the  result. The Xor function----shorthand for "exclusive or"-------returns 1 when its two variables have opposing truth-value and 0 otherwise.Conversely,the Equivalence function returns 1 when the two variables have identical truth-value.The If-x-then-y function returns 1 when x is 0 or when both x and y are 1.The other functions are self-explanatory.