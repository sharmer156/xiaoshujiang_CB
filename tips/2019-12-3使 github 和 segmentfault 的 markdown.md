---
title: 2019-12-3使 github 和 segmentfault 的 markdown 
tags: 
grammar_cjkRuby: true
grammar_mathjax: true
---


无标题文档

# [【小技巧】使 github 和 segmentfault 的 markdown 支持数学公式](https://segmentfault.com/a/1190000019359797)

[小技巧](https://segmentfault.com/t/%E5%B0%8F%E6%8A%80%E5%B7%A7)[markdown](https://segmentfault.com/t/markdown)  阅读约 3 分钟

作者：LogM

本文原载于 <https://segmentfault.com/u/logm/articles> ，不允许转载~

## 1\. 由来

最近在写博客的时候，发现一个问题：

1.  segmentfault不支持markdown行内公式渲染；
2.  github不支持markdown数学公式渲染。

因此，需要想办法正常渲染markdown。否则又要回归繁琐的Github Page了。

## 2\. 解决方法

chrome浏览器可以安装MathJax渲染插件解决，比如：

1.  [MathJax Plugin for Github](https://github.com/orsharir/github-mathjax)
2.  [TeX All the Things](https://github.com/emichael/texthings)

这两个我都用过，可以正常渲染。

第一个插件仅支持github，不需要配置。

第二个插件支持所有的网站，我自己测试在segmentfault上会经常抽风，但多刷新几次页面总有一次能刷出来。右键"Tex All the Things"的图标，选择"选项"，可以进行配置。

所以，对于我的博客中带有数学公式的文章，可以有如下几种方式确保数学公式正常渲染：

1.  使用[插件2](https://github.com/emichael/texthings)在segmentfault上看博客，虽然抽风情况比较严重；
2.  在[我的github](https://github.com/imLogM/notes)上找到对应文章，使用[插件1](https://github.com/orsharir/github-mathjax)查看；
3.  在[我的github](https://github.com/imLogM/notes)上找到对应文章，点击右上角的"Raw"按钮，把源码复制到markdown阅读器查看。

> 注意：这些插件可能对一些网站的脚本功能造成影响，所以不用的时候建议把插件关闭

## 3\. 测试

这里提供一组测试，确认是否完美解决了问题。

<pre>下面参与测试的数学公式的原代码如下：    这是一个行内公式：$P = \frac{C_a^k \cdot C_b^{n-k}}{C_{a+b}^n}$    这是两个单行公式：  $P = \frac{C_a^k \cdot C_b^{n-k}}{C_{a+b}^n}$    $  P = \frac{C_a^k \cdot C_b^{n-k}}{C_{a+b}^n}  $</pre>

下面几行是你的显示效果，如果都显示为数学公式，则说明正常渲染：

这是一个行内公式：`!$P = \frac{C_a^k \cdot C_b^{n-k}}{C_{a+b}^n}$`
```mathjax!
$P = \frac{C_a^k \cdot C_b^{n-k}}{C_{a+b}^n}$    
$  P = \frac{C_a^k \cdot C_b^{n-k}}{C_{a+b}^n}  
$```

这是两个单行公式：

阅读 789 更新于 7月9日