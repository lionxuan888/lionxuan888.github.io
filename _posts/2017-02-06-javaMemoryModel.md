---
layout: post
title: javaMemoryModel
categories: [programming]
tags:
- java memoryModel

#jsr133
[what is java memoryModel](http://www.cs.umd.edu/~pugh/java/memoryModel/jsr-133-faq.htmlfef)
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


What is javaMemoryModel:
The Java Memory Model defines the behavior of volatile and synchronized, and, more importantly, 
ensures that a correctly synchronized Java program runs correctly *on all processor architectures*.
