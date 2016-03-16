---
layout: post
title: Guava Learning
categories: [programming]
tags:
- guava


# Guava ����ѧϰ

------

wiki��https://github.com/google/guava/wiki

## Guava ����ʽ���
��FunctionalExplainedһ�ڣ�guava�����ͱȽ��˺���ʽ�ͳ���ʽ��д��������ָ���˺���ʽ
```python
Even using static imports, even if the Function and the Predicate declarations are moved to a different file, the first implementation is less concise, less readable, and less efficient.
```
�������ܾ���ȷ���������㣺
```python
    Use of functional idioms will result in net savings of lines of code for your entire project. In the example above, the "functional" version used 11 lines, the imperative version 6. Moving the definition of a function to another file, or a constant, does not help.

    For efficiency, you need a lazily computed view of the transformed collection and cannot settle for an explicitly computed collection. Additionally, you have read and reread Effective Java, item 55, and besides following those instructions, you have actually done benchmarking to prove that this version is faster, and can cite numbers to prove it.
```
����ٴ�ǿ����
```python
Please be sure, when using Guava's functional utilities, that the traditional imperative way of doing things isn't more readable. Try writing it out. Was that so bad? Was that more readable than the preposterously awkward functional approach you were about to try?
```
