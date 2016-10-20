---
layout: post
title: CSS Summary
abstract: CSS总结
categories: summary
tags: [summary, css]
hasTag: true
comments: true
---

# CSS

## 盒模型
盒模型(box model)是CSS中的一个重要概念，它是元素大小的呈现方式。
![box](media/box.png)
CSS3中新增了一种盒模型计算方式：box-sizing属性。盒模型默认的值是content-box, 新增的值是padding-box和border-box，几种盒模型计算元素宽高的区别如下：
1. content-box（默认）
布局所占宽度Width：
Width = width + padding-left + padding-right + border-left + border-right
布局所占高度Height:
Height = height + padding-top + padding-bottom + border-top + border-bottom
2. padding-box
布局所占宽度Width：
Width = width(包含padding-left + padding-right) + border-top + border-bottom
布局所占高度Height:
Height = height(包含padding-top + padding-bottom) + border-top + border-bottom
3. border-box
布局所占宽度Width：
Width = width(包含padding-left + padding-right + border-left + border-right)
布局所占高度Height:
Height = height(包含padding-top + padding-bottom + border-top + border-bottom)
margin叠加
当两个或更多个垂直边距相遇时，它们将形成一个外边距。这个外边距的高度等于两个发生叠加的外边距的高度中的较大者。但是注意只有普通文档流中块框的垂直外边距才会发生外边距叠加。行内框、浮动框或绝对定位框之间的外边距不会叠加。
一般来说， 垂直外边距叠加有三种情况：
* 元素自身叠加  当元素没有内容（即空元素）、内边距、边框时，它的上下边距就相遇了，即会产生叠加（垂直方向）。当为元素添加内容、 内边距、边框任何一项，就会取消叠加。
* 相邻元素叠加  相邻的两个元素，如果它们的上下边距相遇，即会产生叠加。
* 包含（父子）元素叠加  包含元素的外边距隔着父元素的内边距和边框，当这两项都不存在的时候，父子元素垂直外边距相邻，产生叠加。添加任何一项即会取消叠加。

## css选择器，哪些可以继承
一、基本选择器
1.	*	通用元素选择器，匹配任何元素
2.	E	标签选择器，匹配所有使用E标签的元素
3.	.info	class选择器，匹配所有class属性中包含info的元素
4.	#footer	id选择器，匹配所有id属性等于footer的元素
二、多元素的组合选择器
5.	E,F	多元素选择器，同时匹配所有E元素或F元素，E和F之间用逗号分隔
6.	E F	后代元素选择器，匹配所有属于E元素后代的F元素，E和F之间用空格分隔
7.	E > F	子元素选择器，匹配所有E元素的子元素F
8.	E + F	毗邻元素选择器，匹配所有紧随E元素之后的同级元素F
三、CSS 2.1 属性选择器
9.	E[att]	匹配所有具有att属性的E元素，不考虑它的值。
10. E[att=val]	  匹配所有att属性等于"val"的E元素
11. E[att~=val]	匹配所有att属性具有多个空格分隔的值、其中一个值等于"val"的E元素
12. E[att|=val]	匹配所有att属性具有多个连字号分隔（hyphen-separated）的值、其中一个值以"val"开头的E元素，主要用于lang属性，比如"en"、"en-us"、"en-gb"等等
四、CSS 2.1中的伪类
13. E:first-child 匹配父元素的第一个子元素
14. E:link	匹配所有未被点击的链接
15. E:visited	匹配所有已被点击的链接
16. E:active 匹配鼠标已经其上按下、还没有释放的E元素
17. E:hover	 匹配鼠标悬停其上的E元素
18. E:focus	 匹配获得当前焦点的E元素
19. E:lang(c) 匹配lang属性等于c的E元素
五、 CSS 2.1中的伪元素
20. E:first-line	匹配E元素的第一行
21. E:first-letter	匹配E元素的第一个字母
22. E:before	在E元素之前插入生成的内容
23. E:after	在E元素之后插入生成的内容
六、CSS 3的同级元素通用选择器
24. E ~ F	匹配任何在E元素之后的同级F元素
八、CSS 3中与用户界面有关的伪类
28. E:enabled 匹配表单中激活的元素
29. E:disabled 匹配表单中禁用的元素
30. E:checked 匹配表单中被选中的radio（单选框）或checkbox（复选框）元素
31. E::selection	匹配用户当前选中的元素
九、CSS 3中的结构性伪类
32. E:root	匹配文档的根元素，对于HTML文档，就是HTML元素
33. E:nth-child(n)	匹配其父元素的第n个子元素，第一个编号为1
34. E:nth-last-child(n)	匹配其父元素的倒数第n个子元素，第一个编号为1
35. E:nth-of-type(n)	与:nth-child()作用类似，但是仅匹配使用同种标签的元素
36. E:nth-last-of-type(n)	与:nth-last-child() 作用类似，但是仅匹配使用同种标签的元素
37. E:last-child	匹配父元素的最后一个子元素，等同于:nth-last-child(1)
38. E:first-of-type	匹配父元素下使用同种标签的第一个子元素，等同于:nth-of-type(1)
39. E:last-of-type	匹配父元素下使用同种标签的最后一个子元素，等同于:nth-last-of-type(1)
40. E:only-child	匹配父元素下仅有的一个子元素，等同于:first-child:last-child或 :nth-child(1):nth-last-child(1)
41. E:only-of-type	匹配父元素下使用同种标签的唯一一个子元素，等同于:first-of-type:last-of-type或 :nth-of-type(1):nth-last-of-type(1)
42. E:empty	匹配一个不包含任何子元素的元素，注意，文本节点也被看作子元素
十、CSS 3的反选伪类
43. E:not(s)	匹配不符合当前选择器的任何元素

## CSS优先级算法如何计算
* 样式的优先级算法
原则一：继承不如指定
原则二：#id > .class > 标签选择符
原则三：越具体越强大
* CSS优先级的计算规则如下：
元素标签中定义的样式（Style属性）,加1,0,0,0
每个ID选择符(如 #id),加0,1,0,0
每个Class选择符(如 .class)、每个属性选择符(如 [attribute=])、每个伪类(如 :hover)加0,0,1,0
每个元素选择符（如p）或伪元素选择符(如 :firstchild)等，加0,0,0,1
然后，将这四个数字分别累加，就得到每个CSS定义的优先级的值，
然后从左到右逐位比较大小，数字大的CSS样式的优先级就高。
* 注意：
!important声明的样式优先级最高，如果冲突再进行计算。
如果优先级相同，则选择最后出现的样式。
继承得到的样式的优先级最低。

## display有哪些值？说明他们的作用
```
block         象块类型元素一样显示。
none          缺省值。象行内元素类型一样显示。
inline-block  象行内元素一样显示，但其内容象块类型元素一样显示。
list-item     象块类型元素一样显示，并添加样式列表标记。
table         此元素会作为块级表格来显示
inherit       规定应该从父元素继承 display 属性的值
```
## position的值relative和absolute定位原点是什么
* absolute  
生成绝对定位的元素，相对于值不为 static的第一个父元素进行定位。
* fixed （老IE不支持）
生成绝对定位的元素，相对于浏览器窗口进行定位。
* relative
生成相对定位的元素，相对于其正常位置进行定位。
* static
默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）
* inherit
规定从父元素继承position属性的值。

## CSS3有哪些新特性
* 新增各种CSS选择器 （: not(.input)：所有 class 不是“input”的节点）
* 圆角 （border-radius:8px）
* 多列布局 （multi-column layout）
* 阴影和反射 （Shadow\Reflect）
* 文字特效 （text-shadow、）
* 文字渲染 （Text-decoration）
* 线性渐变 （gradient）
* 旋转 （transform）
  
## 用纯CSS创建一个三角形的原理是什么
```
把上、左、右三条边隐藏掉（颜色设为 transparent）
#demo {
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent transparent red transparent;
}
```
## webpack
