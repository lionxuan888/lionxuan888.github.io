---
layout: post
title: javaMemoryModel
categories: [programming]
tags:
- java memoryModel
---

#jsr133
[what is java memoryModel](http://www.cs.umd.edu/~pugh/java/memoryModel/jsr-133-faq.html)
[memoryModel](http://docs.oracle.com/javase/specs/jls/se8/html/jls-17.html#jls-17.4)

- What is a memory model, anyway?
- Do other languages, like C++, have a memory model?
- What is JSR 133 about?
- What is meant by reordering?
- What was wrong with the old memory model?
- What do you mean by incorrectly synchronized?
- What does synchronization do?
- How can final fields appear to change their values?
- How do final fields work under the new JMM?
- What does volatile do?
- Does the new memory model fix the "double-checked locking" problem?
- What if I'm writing a VM?
- Why should I care?


比较有代表性的介绍
What is javaMemoryModel:

1. The Java Memory Model defines the behavior of volatile and synchronized, and, more importantly, 

ensures that a correctly synchronized Java program runs correctly *on all processor architectures*;

2. The Java Memory Model was an ambitious undertaking; 

it was the first time that a programming language specification 

attempted to incorporate a memory model which could provide consistent semantics 

for concurrency across a variety of architectures. Unfortunately, 

defining a memory model which is both consistent and intuitive proved far more difficult than expected. 

JSR 133 defines a new memory model for the Java language which fixes the flaws of the earlier memory model. 

In order to do this, the semantics of final and volatile needed to change.

