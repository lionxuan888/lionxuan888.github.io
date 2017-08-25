---
layout: post
title: regularExpression
categories: [programming]
tags:
- java regularExpression 正则表达式
---

#[Wiki](https://en.wikipedia.org/wiki/Regular_expression)
 

- What is regularExpression:

    A regular expression, regex or regexp[1] (sometimes called a rational expression)[2][3] is, in theoretical computer science and formal language theory, 
    a sequence of characters that define a search pattern. 
    Usually this pattern is then used by string searching algorithms for "find" or "find and replace" operations on strings.

- 有什么作用
```
Regular expressions are used in search engines, search and replace dialogs of word processors 
and text editors, in text processing utilities such as sed and AWK and in lexical analysis.
 Many programming languages provide regex capabilities, built-in, or via libraries.
 ```
 - Patterns 
   
   正则表达式组成结构，参看wiki，两部分:meta character or  regular character 
   
   如何实现
   
 汤姆森构造，不确定性有限自动机
 ```
 A regex processor translates a regular expression in the above syntax into an internal representation 
 
 which can be executed and matched against a string representing the text being searched in.
 
  One possible approach is the Thompson's construction algorithm to construct a nondeterministic finite automaton (NFA), 
  
  which is then made deterministic and the resulting DFA is run on the target text string 
  
  to recognize substrings that match the regular expression. The picture shows the NFA scheme N(s*) 
  
  obtained from the regular expression s*, where s denotes a simpler regular expression in turn, 
  
 which has already been recursively translated to the NFA N(s).
 ```
 
 - Standards 标准
 
 主要是BRE和ERE
 
 ```
 The IEEE POSIX standard has three sets of compliance: BRE (Basic Regular Expressions),[25] ERE (Extended Regular Expressions), 
 
 and SRE (Simple Regular Expressions). SRE is deprecated,[26] in favor of BRE, 
 
 as both provide backward compatibility. The subsection below covering the character classes applies to both BRE and ERE
 ```
 1. linux 的grep命令有选项，-E 和 -G 就是选择哪个标准
 2. perl正则已经演化为真正意义上的标准了，由于其丰富和强大的自动化表达式。
 perl还提供了很多功能，比如懒加载，回溯，命名式捕获组和循环模式等，所有这些都是都对POSIX BRE/ERE强有力的补充
 Java, JavaScript, Python等众多语言都是使用的perl like
 ```
 Perl regexes have become a de facto standard, having a rich and powerful set of atomic expressions.
 
  Perl has no "basic" or "extended" levels, where the ( ) and { } may or may not have literal meanings. 
  
  They are always metacharacters, as they are in "extended" mode for POSIX. To get their literal meaning, you escape them. 
  
  Other metacharacters are known to be literal or symbolic based on context alone. 
   
  Perl offers much more functionality: "lazy" regexes, backtracking, named capture groups, 
  
  and recursive patterns,  all of which are powerful additions to POSIX BRE/ERE. (See lazy matching below.)
  ```
  
  详细的可以细读[Wiki](https://en.wikipedia.org/wiki/Regular_expression)
  
  
  
  - java Pattern里的special constructs 
  看例子好像是对表达式匹配的值的二次限定，即对后面正则的二次限定范围
  比如：
  ```
  we wanted to know if our input string contains the word “incident” 
  but that the word “theft” should not be found anywhere. We can use a negative look-ahead to 
  ensure that there are no occurrences.
  “(?!.*theft).*incident.*”
  ```
  http://www.ocpsoft.org/opensource/guide-to-regular-expressions-in-java-part-2/
  
  ```
    Look-ahead/behind constructs (non-capturing)
  (?:X) 			X, as a non-capturing group
  (?=X) 			X, via zero-width positive look-ahead
  (?!X) 			X, via zero-width negative look-ahead
  (?<=X) 			X, via zero-width positive look-behind
  (?<!X) 			X, via zero-width negative look-behind
  (?<X) 			X, as an independent, non-capturing group
  So what does this all mean? What does a look-ahead really do for me? Say, for example, 
  we wanted to know if our input string contains the word “incident” but that the word “theft” 
  should not be found anywhere. We can use a negative look-ahead to ensure that there are no occurrences.
  “(?!.*theft).*incident.*”
  This expression exhibits the following behavior:
  "There was a crime incident"			matches
  "The incident involved a theft"			does not match
  "The theft was a serious incident"		does not match
 ```
 
-- java的量词

http://blog.csdn.net/carolzhang8406/article/details/6726546

```
贪婪量词：
先看整个字符串是不是一个匹配。如果没有发现匹配，它去掉最后字符串中的最后一个字符，并再次尝试。如果还是没有发现匹配，那么    再次去掉最后一个字符串，这个过程会一直重复直到发现一个匹配或者字符串不剩任何字符。简单量词都是贪婪量词。
    惰性量词：
先看字符串中的第一个字母是不是一个匹配，如果单独着一个字符还不够，就读入下一个字符，组成两个字符的字符串。如果还没有发现匹配，惰性量词继续从字符串中添加字符直到发现一个匹配或者整个字符串都检查过也没有匹配。惰性量词和贪婪量词的工作方式恰好相反。
    支配量词：
只尝试匹配整个字符串。如果整个字符串不能产生匹配，不做进一步尝试。
```