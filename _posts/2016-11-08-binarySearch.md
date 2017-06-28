---
layout: post
title: 二叉树
categories: [programming]
tags:
- data structure
---
先来一堆概念
#二叉树定义[wiki](https://zh.wikipedia.org/wiki/二叉树 "wiki" )
- 二叉树（英语：Binary tree）是每个节点最多有两个子树的树结构
- 与树不同，树的节点个数至少为1，而二叉树的节点个数可以为0；树中节点的最大度数没有限制，而二叉树节点的最大度数为2

#满二叉树

#完全二叉树

#二叉搜索树[wiki](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%85%83%E6%90%9C%E5%B0%8B%E6%A8%B9)

二叉查找树（英语：Binary Search Tree），也称二叉搜索树、有序二叉树（英语：ordered binary tree），排序二叉树（英语：sorted binary tree），是指一棵空树或者具有下列性质的二叉树：
1. 任意节点的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
2. 任意节点的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
3. 任意节点的左、右子树也分别为二叉查找树；
4. 没有键值相等的节点。

#平衡二叉树
典型的代表有avl和红黑树
红黑树参照：
[https://github.com/julycoding/The-Art-Of-Programming-By-July/blob/master/ebook/zh/03.01.md](https://github.com/julycoding/The-Art-Of-Programming-By-July/blob/master/ebook/zh/03.01.md)

{% highlight python3 %}
LEFT-ROTATE(T, x)  
1  y ← right[x] ▹ Set y.  
2  right[x] ← left[y]      ▹ Turn y's left subtree into x's right subtree.  
3  p[left[y]] ← x  
4  p[y] ← p[x]             ▹ Link x's parent to y.  
5  if p[x] = nil[T]  
6     then root[T] ← y  
7     else if x = left[p[x]]  
8             then left[p[x]] ← y  
9             else right[p[x]] ← y  
10  left[y] ← x             ▹ Put x on y's left.  
11  p[x] ← y  
{% endhighlight %}