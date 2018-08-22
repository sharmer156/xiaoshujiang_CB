---
title: Python3 字符编码
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


<div id="post_detail">
<!--done-->
<div id="topics">
	<div class = "post">
		<h1 class = "postTitle">
			<a id="cb_post_title_url" class="postTitle2" href="https://www.cnblogs.com/284628487a/p/5584714.html">Python3 字符编码</a>
		</h1>
		<div class="clear"></div>
		<div class="postBody">
			<div id="cnblogs_post_body" class="blogpost-body"><h3>编码</h3>
<p>字符串是一种数据类型，但是，字符串比较特殊的是还有一个编码问题。</p>
<p>因为计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用8个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），如果要表示更大的整数，就必须用更多的字节。比如两个字节可以表示的最大整数是<code>65535</code>，4个字节可以表示的最大整数是<code>4294967295</code>。</p>
<p>由于计算机是美国人发明的，因此，最早只有127个字母被编码到计算机里，也就是大小写英文字母、数字和一些符号，这个编码表被称为<code>ASCII</code>编码，比如大写字母<code>A</code>的编码是<code>65</code>，小写字母<code>z</code>的编码是<code>122</code>。</p>
<h3>Unicode</h3>
<p>Unicode把所有语言都统一到一套编码里，这样就不会再有乱码问题了。</p>
<p>Unicode标准也在不断发展，但最常用的是用两个字节表示一个字符（如果要用到非常偏僻的字符，就需要4个字节）。现代操作系统和大多数编程语言都直接支持Unicode。</p>
<p>现在，捋一捋ASCII编码和Unicode编码的区别：<span style="color: #ff0000;">ASCII编码是1个字节</span>，而<span style="color: #ff0000;">Unicode编码通常是2个字节</span>。</p>
<p>字母<code>A</code>用ASCII编码是十进制的<code>65</code>，二进制的<code>01000001</code>；</p>
<p>字符<code>0</code>用ASCII编码是十进制的<code>48</code>，二进制的<code>00110000</code>，注意字符<code>'0'</code>和整数<code>0</code>是不同的；</p>
<p>汉字已经超出了ASCII编码的范围，用Unicode编码是十进制的<code>20013</code>，二进制的<code>01001110 00101101</code>。</p>
<p>如果把ASCII编码的<code>A</code>用Unicode编码，只需要在前面补0就可以，因此，<code>A</code>的Unicode编码是<code>00000000 01000001</code>。&nbsp;</p>
<p>新的问题又出现了：如果统一成Unicode编码，乱码问题从此消失了。但是，如果你写的文本基本上全部是英文的话，用Unicode编码比ASCII编码需要多一倍的存储空间，在存储和传输上就十分不划算。</p>
<p>所以，又出现了把Unicode编码转化为&ldquo;可变长编码&rdquo;的<code>UTF-8</code>编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。如果你要传输的文本包含大量英文字符，用UTF-8编码就能节省空间：</p>
<table class="uk-table">
<tbody>
<tr><th>字符</th><th>ASCII</th><th>Unicode</th><th>UTF-8</th></tr>
<tr>
<td>A</td>
<td>01000001</td>
<td>00000000 01000001</td>
<td>01000001</td>
</tr>
<tr>
<td>中</td>
<td>x</td>
<td>01001110 00101101</td>
<td>11100100 10111000 10101101</td>
</tr>
</tbody>
</table>
<p>从上面的表格还可以发现，UTF-8编码有一个额外的好处，就是ASCII编码实际上可以被看成是UTF-8编码的一部分，所以，大量只支持ASCII编码的历史遗留软件可以在UTF-8编码下继续工作。</p>
<p>搞清楚了ASCII、Unicode和UTF-8的关系，我们就可以总结一下现在计算机系统通用的字符编码工作方式：</p>
<p>在<span style="color: #ff0000;">计算机内存中，统一使用Unicode编码</span>，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。</p>
<p>用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件：</p>
<p><img src="http://www.liaoxuefeng.com/files/attachments/001387245992536e2ba28125cf04f5c8985dbc94a02245e000/0" alt="" width="307" height="278" /></p>
<p>浏览网页的时候，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器：</p>
<p><img src="http://www.liaoxuefeng.com/files/attachments/001387245979827634fd6204f9346a1ae6358d9ed051666000/0" alt="" width="302" height="266" /></p>
<p>所以你看到很多网页的源码上会有类似<code>&lt;meta charset="UTF-8" /&gt;</code>的信息，表示该网页正是用的UTF-8编码。</p>
<h3 id="python-">Python的字符串</h3>
<p>在最新的Python 3版本中，字符串是以Unicode编码的，也就是说，Python的字符串支持多语言，例如：</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; <span style="color: #0000ff;">print</span>(<span style="color: #800000;">'</span><span style="color: #800000;">包含中文的str</span><span style="color: #800000;">'</span><span style="color: #000000;">)
包含中文的str</span></pre>
</div>
<p>对于单个字符的编码，Python提供了<code>ord()</code>函数获取字符的整数表示，<code>chr()</code>函数把编码转换为对应的字符：</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; ord(<span style="color: #800000;">'</span><span style="color: #800000;">A</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span>65
&gt;&gt;&gt; ord(<span style="color: #800000;">'</span><span style="color: #800000;">中</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span>20013
&gt;&gt;&gt; chr(66<span style="color: #000000;">)
</span><span style="color: #800000;">'</span><span style="color: #800000;">B</span><span style="color: #800000;">'</span>
&gt;&gt;&gt; chr(25991<span style="color: #000000;">)
</span><span style="color: #800000;">'</span><span style="color: #800000;">文</span><span style="color: #800000;">'</span></pre>
</div>
<p>如果知道字符的整数编码，还可以用十六进制这么写<code>str</code></p>
<div class="cnblogs_code">
<pre>'\u4e2d\u6587' // 中文</pre>
</div>
<h3>byte</h3>
<p>由于Python的字符串类型是<code>str</code>，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把<code>str</code>变为以字节为单位的<code>bytes</code>。</p>
<p>Python对<code>bytes</code>类型的数据用带<code>b</code>前缀的单引号或双引号表示：</p>
<div class="cnblogs_code">
<pre>x = b'ABC'</pre>
</div>
<p><code>要注意区分<code>'ABC'</code>和<code>b'ABC'</code>，前者是<code>str</code>，后者虽然内容显示得和前者一样，但<code>bytes</code>的每个字符都只占用一个字节。</code>&nbsp;</p>
<p>以Unicode表示的<code>str</code>通过<code>encode()</code>方法可以编码为指定的<code>bytes</code>，例如：</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">ABC</span><span style="color: #800000;">'</span>.encode(<span style="color: #800000;">'</span><span style="color: #800000;">ascii</span><span style="color: #800000;">'</span><span style="color: #000000;">)
b</span><span style="color: #800000;">'</span><span style="color: #800000;">ABC</span><span style="color: #800000;">'</span>
&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">中文</span><span style="color: #800000;">'</span>.encode(<span style="color: #800000;">'</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">'</span><span style="color: #000000;">)
b</span><span style="color: #800000;">'</span><span style="color: #800000;">\xe4\xb8\xad\xe6\x96\x87</span><span style="color: #800000;">'</span>
&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">中文</span><span style="color: #800000;">'</span>.encode(<span style="color: #800000;">'</span><span style="color: #800000;">ascii</span><span style="color: #800000;">'</span><span style="color: #000000;">)
Traceback (most recent call last):
  File </span><span style="color: #800000;">"</span><span style="color: #800000;">&lt;stdin&gt;</span><span style="color: #800000;">"</span>, line 1, <span style="color: #0000ff;">in</span> &lt;module&gt;<span style="color: #000000;">
UnicodeEncodeError: </span><span style="color: #800000;">'</span><span style="color: #800000;">ascii</span><span style="color: #800000;">'</span> codec can<span style="color: #800000;">'</span><span style="color: #800000;">t encode characters in position 0-1: ordinal not in range(128)</span></pre>
</div>
<p>纯英文的<code>str</code>可以用<code>ASCII</code>编码为<code>bytes</code>，内容是一样的，含有中文的<code>str</code>可以用<code>UTF-8</code>编码为<code>bytes</code>。含有中文的<code>str</code>无法用<code>ASCII</code>编码，因为中文编码的范围超过了<code>ASCII</code>编码的范围，Python会报错。</p>
<p>在<code>bytes</code>中，无法显示为ASCII字符的字节，用<code>\x##</code>显示。</p>
<p>反过来，如果我们从网络或磁盘上读取了字节流，那么读到的数据就是<code>bytes</code>。要把<code>bytes</code>变为<code>str</code>，就需要用<code>decode()</code>方法：</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; b<span style="color: #800000;">'</span><span style="color: #800000;">ABC</span><span style="color: #800000;">'</span>.decode(<span style="color: #800000;">'</span><span style="color: #800000;">ascii</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span><span style="color: #800000;">'</span><span style="color: #800000;">ABC</span><span style="color: #800000;">'</span>
&gt;&gt;&gt; b<span style="color: #800000;">'</span><span style="color: #800000;">\xe4\xb8\xad\xe6\x96\x87</span><span style="color: #800000;">'</span>.decode(<span style="color: #800000;">'</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span><span style="color: #800000;">'</span><span style="color: #800000;">中文</span><span style="color: #800000;">'</span></pre>
</div>
<p>要计算<code>str</code>包含多少个字符，可以用<code>len()</code>函数</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; len(<span style="color: #800000;">'</span><span style="color: #800000;">ABC</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span>3
&gt;&gt;&gt; len(<span style="color: #800000;">'</span><span style="color: #800000;">中文</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span>2</pre>
</div>
<p><code>len()</code>函数计算的是<code>str</code>的字符数，如果换成<code>bytes</code>，<code>len()</code>函数就计算字节数</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; len(b<span style="color: #800000;">'</span><span style="color: #800000;">ABC</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span>3
&gt;&gt;&gt; len(b<span style="color: #800000;">'</span><span style="color: #800000;">\xe4\xb8\xad\xe6\x96\x87</span><span style="color: #800000;">'</span><span style="color: #000000;">)
</span>6
&gt;&gt;&gt; len(<span style="color: #800000;">'</span><span style="color: #800000;">中文</span><span style="color: #800000;">'</span>.encode(<span style="color: #800000;">'</span><span style="color: #800000;">utf-8</span><span style="color: #800000;">'</span><span style="color: #000000;">))
</span>6</pre>
</div>
<p>1个中文字符经过UTF-8编码后通常会占用3个字节，而1个英文字符只占用1个字节。</p>
<p>在操作字符串时，我们经常遇到<code>str</code>和<code>bytes</code>的互相转换。为了避免乱码问题，应当始终坚持使用UTF-8编码对<code>str</code>和<code>bytes</code>进行转换。</p>
<p>Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行</p>
<div class="cnblogs_code">
<pre><span style="color: #008000;">#</span><span style="color: #008000;">!/usr/bin/env python3</span><span style="color: #008000;">
#</span><span style="color: #008000;"> -*- coding: utf-8 -*-</span></pre>
</div>
<p>第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。</p>
<h3>格式化：</h3>
<p>在Python中，采用的格式化方式和C语言是一致的，用<code>%</code>实现，举例如下：</p>
<pre>format % (...params)</pre>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">Hello, %s</span><span style="color: #800000;">'</span> % <span style="color: #800000;">'</span><span style="color: #800000;">world</span><span style="color: #800000;">'</span>
<span style="color: #800000;">'</span><span style="color: #800000;">Hello, world</span><span style="color: #800000;">'</span>
&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">Hi, %s, you have $%d.</span><span style="color: #800000;">'</span> % (<span style="color: #800000;">'</span><span style="color: #800000;">Michael</span><span style="color: #800000;">'</span>, 1000000<span style="color: #000000;">)
</span><span style="color: #800000;">'</span><span style="color: #800000;">Hi, Michael, you have $1000000.</span><span style="color: #800000;">'</span></pre>
</div>
<p><code>%</code>运算符就是用来格式化字符串的。在字符串内部，<code>%s</code>表示用字符串替换，<code>%d</code>表示用整数替换，<code>%x</code>表示16进制整数，有几个<code>%?</code>占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个<code>%?</code>，括号可以省略。</p>
<p>格式化整数和浮点数还可以指定是否补0和整数与小数的位数：</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">%2d-%02d</span><span style="color: #800000;">'</span> % (3, 1<span style="color: #000000;">)
</span><span style="color: #800000;">'</span><span style="color: #800000;"> 3-01</span><span style="color: #800000;">'</span>
&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">%.2f</span><span style="color: #800000;">'</span> % 3.1415926
<span style="color: #800000;">'</span><span style="color: #800000;">3.14</span><span style="color: #800000;">'</span></pre>
</div>
<p>有些时候，字符串里面的<code>%</code>是一个普通字符怎么办？这个时候就需要转义，用<code>%%</code>来表示一个<code>%</code>：</p>
<div class="cnblogs_code">
<pre>&gt;&gt;&gt; <span style="color: #800000;">'</span><span style="color: #800000;">growth rate: %d %%</span><span style="color: #800000;">'</span> % 7
<span style="color: #800000;">'</span><span style="color: #800000;">growth rate: 7 %</span><span style="color: #800000;">'</span></pre>
</div>
<p>&nbsp;</p></div><div id="MySignature"></div>
<div class="clear"></div>
<div id="blog_post_info_block">
<div id="BlogPostCategory"></div>
<div id="EntryTag"></div>
<div id="blog_post_info">
</div>
<div class="clear"></div>
<div id="post_next_prev"></div>
</div>

