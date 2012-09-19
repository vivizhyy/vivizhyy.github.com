---
layout: default
title: 折腾 ICTCLA 分词以及 Lucene SmartCn 分词
---

好吧，分词在中文里头的确是个令人头疼的事情，感觉计算机就像以前那个只有[句读](http://baike.baidu.com/view/331315.htm)年代的弱智学生一样，得要先生教句读，然后才会读，当然啦，先生没有教的不会句读啦，只会读成单字。  
[ICTCLA](http://www.ictclas.org/) 是用 C 写成的，只支持 32 位系统（那个所谓的 64 位版本，其实也是 32 位的，只是该作者的 Intel 86 系列能够调用 32 位版本的，如果你是 AMD 64 位就只能望洋兴叹啦）。ICTCLA 的使用很简单，文档写的很清楚，照做就行了。下面是一段利用 ICTCLA 分词的 java 代码：  
<script src="https://gist.github.com/3749300.js?file=Tagger.java"></script>  
  
关于 Lucene 的 SmartCn, [原理](http://blog.csdn.net/lgnlgn/article/details/5669855)跟 ICTCLA 分词一样一样的，只是简化了些，比如：  
<ul>
<li>不能登录未识别词</li>
<li>对时间词没有特殊优化</li>
<li>对人名没有特殊优化</li>
<li>不能扩展词库</li>
<li>...</li>
</ul>
但是需要注意的是 Lucene 3.x 之后，TokenStream 里面的 Token 就被 Attributes 取代了，原有的一些找 Token 的方法（比如[这个](http://www.diybl.com/course/3_program/java/javaxl/2008926/145584.html)）已经不再适用啦，取而代之的可用用 `ts.getAttribute(CharTermAttribute.class)` 代替：  
<script src="https://gist.github.com/3749300.js?file=TestSmartCn.java"></script>  
  
但是，空有分词的程序不行沙，得要有词典（就是老师教句读的那个积累啦）才能分得准。老师为啥能读的准咧，因为老师积累的多。所以咧，这个分词要分得准，还得词典够大才行。谁的词典大？百度、搜狗、腾讯的都行，所以，下面的代码是用来解析搜狗词库文件的啦：  
<script src="https://gist.github.com/3749438.js?file=SouGouDic.java"></script>
<script src="https://gist.github.com/3749438.js?file=SouGouDicParser.java"></script>  
关于各家词典文件的格式描述，请猛击[这里](http://www.wumii.com/item/1xLNiCV0)查看