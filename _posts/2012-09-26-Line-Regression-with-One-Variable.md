---
layout: default
title: Line Regression with One Variable
---

开始看 Stanford University 的机器学习[课程](https://class.coursera.org/ml/lecture/index)。讲的还是蛮简单易懂的。

###Model representation###
无监督学习和监督学习：Line Regression 是一种监督学习。  
hypothesis 就是那个映射 x(feature) 到 y(target) 的东东啦~  

###Cost function###
要选择合适的参数，让 h<sub>θ</sub>(x) 和训练数据中的 y 更接近。

####intuition I####
Cost function: J(θ<sub>0</sub>, θ<sub>1</sub>) = (1/2m) * ∑( h<sub>θ</sub> ( x<sup><small>i</small></sup> ) - y<sup><small>i</small></sup> )<sup>2</sup>  
  
Goal: 最小化 J(θ<sub>0</sub>, θ<sub>1</sub>)  
####intuition II####
讲了啥？？？
###Gradient descent###
从某一点开始，然后逐渐的改变 (θ<sub>0</sub>, θ<sub>1</sub>)，使得 J(θ<sub>0</sub>, θ<sub>1</sub>) 能达到最小值。但是这样可能找到局部最小值而不是全局最小值。
<pre>rep</pre>