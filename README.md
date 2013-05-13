9 可视化格式模型
===
## 9.1 可视化格式模型介绍
本章和下章描述可视化格式模型：用户代理为视觉媒体处理文档树的方式。

在可视化格式模型中，文档树中的每一个元素按照盒模型生成0个或多个盒。这些盒的布局由以下定义决定：

* 盒子的尺寸和类型
* 定位方案（正常流，浮动和绝对定位）
* 文档树中的元素之间的关系
* 外部信息（例如，视窗大小，图片元素的本身尺寸等）

本章和下章定义的属性应用于页面媒体和延伸媒体，然而，在页面媒体中，margin属性有不同的意义（详见页面模型）。

可视化格式模型没有明确说明格式模型的所有特征（例如，它没有明确letter-spacing算法）。因此，用户代理对这些规范没有覆盖到的格式化问题可能有不同的实现。


### 9.1.1 视窗

延展媒体的用户代理通常提供一个视窗（屏幕上一个窗口或者其他显示区域）供用户翻阅文档。当视窗大小改变的时候用户代理会改变文档布局（见初始化包含块）。

当视窗比文档渲染完后的画布区域小时，用户代理应该提供一个滚动机制。每个画布至少应该有一个视窗，但用户代理可以渲染出多个画布（例如：给同一个文档提供不同的显示）。

### 9.1.2 包含块（containing blocks）

延展媒体的用户代理通常提供一个视窗（屏幕上一个窗口或者其他显示区域）供用户翻阅文档。当视窗大小改变的时候用户代理会改变文档布局（见初始化包含块）。

当视窗比文档渲染完后的画布区域小时，用户代理应该提供一个滚动机制。每个画布至少应该有一个视窗，但用户代理可以渲染出多个画布（例如：给同一个文档提供不同的显示）。


## 9.2 控制盒的产生

延展媒体的用户代理通常提供一个视窗（屏幕上一个窗口或者其他显示区域）供用户翻阅文档。当视窗大小改变的时候用户代理会改变文档布局（见初始化包含块）。

当视窗比文档渲染完后的画布区域小时，用户代理应该提供一个滚动机制。每个画布至少应该有一个视窗，但用户代理可以渲染出多个画布（例如：给同一个文档提供不同的显示）。


### 9.2.1 块级元素（block-level elements）和块盒（block boxes）

块级元素（block-level elements）是指那些在源文档中以块方式来格式化视觉样式的元素（例如，paragraphs）。下面的这些display属性的值使得一个元素变成块级元素：’block’，’list-item’和’table’。

块级盒（block-level boxes）是指那些作用在一个块格式化上下文中的盒。每个块级元素生成一个主要块级盒，这个块级盒包含了块级元素的子孙盒以及它们生成的内容，并且同时参与了所有的定位方案。除了主要块级盒外，有些块级元素还可能会生成额外的盒子：比如’list-item’元素。这些额外的盒子与主要块级盒有同样的行为。

除了table盒之外，其他的盒将在下面的章节进行描述，而抛开元素来说，一个块级盒也是一个块容器(盒)（block container box）。一个块容器(盒)只能包含块级盒或者建立一个只能包含行内盒的行内格式化上下文。不是所有的块容器(盒)都是块级盒：non-replaced 行内盒和non-relaced table cell是块容器(盒)但不是块级盒。同时是块容器的块级盒称为块盒。

“块级盒block-level box”, “块容器(盒)block container box ”，”块盒block box”这三个术语有时候被明确的简写成”块block”。


#### 9.2.1.1 匿名块盒（anonymous block boxes）

文档中这样的代码：
```html
<div>
some text
<p>more test
</div>
```
（并且假设div和p都有属性“display：block”），div看起来有行内内容跟块内容。为了把定义格式化变得简单，我们假设这里存在一个匿名块盒包围“some text”。


换句话说：如果一个块容器（盒）（就像上面div生成的那个）内部有一个块级盒（就像上面的P），那么我们强制它的内部必须只能有块级盒。

当一个行内盒包含一个流内的块级盒时，该行内盒（和它的行内祖先）





### 9.2.2 行内级元素（inline-level elements）和行内盒（inline boxes）



####　9.2.1.1 匿名行内盒（anonymous inline boxes）



### 9.2.3 run-in boxes



### 9.2.4 “display”属性




## 9.3 定位方案
在CSS2.1中，盒可以按照三种定位方案进行布局：

1. 正常流。在CSS2.1中，正常流包含块级盒的块格式（block-formatting），行内盒的行内格式（inline-foramtting），以及块级和行内级盒的相对定位（relative positioning）。
2. 浮动。在浮动模型中，盒首先根据正常流布局，然后取出流尽可能的往左或往右排布。内容会随着浮动的边流动。
3. 绝对定位。在绝对定位模型中，盒子彻底从正常流中被移除（它不再对后面的兄弟节点产生影响）并且被赋予一个与包含块相关的位置。

如果一个元素被浮动，绝对定位或者它是一个根元素，那么它被称为流外元素（out of flow）。如果一个元素不是流外元素，那么它被成为流内元素。一个元素A的流是指由A和那些最接近流外元素，祖先是A的流内元素组成的集合。

注意：CSS2.1的定位方案让作者通过避免那些为了实现布局效果的深度陷阱（例如： 不可见的图片），从而使他们的文档更容易理解。

### 9.3.1 选择一种定位方案：“position”属性


### 9.3.2 盒偏移：“top”，“right”，“bottom”，“left”



## 9.4 正常流（normal flow）
在正常流中的盒属于一个格式上下文（formatting context），可能是块或者行内，但不能两者都是。块级盒参与一个块格式化上下文（block formatting context）。行内盒参与一个行内格式化上下文（inline formatting context）。

### 9.4.1 块格式化上下文（block formatting context）
浮动，绝对定位元素，不是块盒的块容器（例如inline-blocks, table-cells和table-captions）和包含除了“visible”以外值的“overflow”属性的块盒（除非当这个值被传播到视窗）会为它们的内容建立一个新的块格式化上下文。

在一个块格式化上下文中，盒从包含块顶部开始，按垂直方向一个接一个进行布局。两个相邻兄弟盒之间的垂直距离由“margin”属性决定。在块格式化上下文中紧邻的块级盒之间的垂直margin会折叠。

在一个块格式化上下文中，每个盒的左外边缘和包含块的左边缘对齐（在从右到左的格式中，右边缘对齐）。这甚至对于浮动元素也是正确的（尽管由于浮动a box’s line boxes会收缩），除非这个盒子建立一个新的块格式化上下文（in which case the box itself may due to the floats）。



### 9.4.2 行内格式化上下文（inline formatting context）
在一个行内格式化上下文中，盒从包含块的顶部开始，按水平方向一个接一个进行布局。水平方向的margin，borders和padding被展现在这些盒之间。盒可以在垂直方向上按照不同的方式对齐：按照它们的底部或者顶部对齐，或者按照他们内部的文本基线（baseline）对齐。包含这些构成一条线的盒子的矩形区域称为line box。

line box的宽度取决于包含块和浮动的存在。line box的高度取决于本章行高的计算中给出的规则。
一个line box对于它包含的所有盒总是足够高的。可是，它也可能高于它包含的盒中最高的那个（如果，举个例子，boxes are aligned so that baseline up）。当一个盒B的高度小于包含它的line box的高度时，B在这个line box中的垂直方向对齐方式取决于“vertical-align”属性。当几个行内级盒无法在一个line box中处于一个水平线时，它们被分发给两个或者更多的垂直栈（vertically-stacked）的line box。也就是说，一个段落时line box的一个垂直栈（vertical stack）。line box被紧密的堆叠（除非特别声明）但永远不会重叠。

总的来说，一个line box的左边缘和它的包含块的左边缘对齐而且它的右边缘和包含块的右边缘对齐。但是，浮动的盒会在包含盒的边缘和line box的边缘之间。也就是说，虽然在一个相同行内格式话上下文中的line box普遍拥有相同的宽度（包含盒的宽度），但是由于浮动元素导致水平方向的可用空间的减少，它们可能在宽度方面有差异。在同一个行内格式化上下文中的line box普遍在高度上面有差异（例如，当其他元素只包含文本而有一个元素包含一个高的图片时）。

当在一行中的所有行内级盒的宽度和比包含他们的line box小时，它们在line box中的水平位置的分配方式取决于“text-align”属性。如果这个属性的值是“justify”，用户代理尽可能将拉伸行内盒中的单词和空白（但inline-table和inline-block盒不会）。

当一个行内盒超出一个line box的宽度，它被分割成多个盒并且这些盒被分配到多个line box中。如果一个行内盒无法被分割（例如，如果这个行内盒包含了一个字符，或者语言中规定的单词折断规则不允许它在行内盒中被折断，或者如果这个行内盒被一个white-space为nowrap的值所影响，或者是一个pre），那么行内盒会溢出line box。

当一个行内盒被分割开，margins，borders和padding在分割发生的地方被忽略（没有视觉效果）。

由于双向文本处理方式（bidirectional text processing），相同line box中的行内盒也可能被分割成多个盒。

xxxxx



### 9.4.3 相对定位




## 9.5 浮动
浮动是指一个盒在当前行中被换到左边或者右边。浮动最有意思的特点是内容将沿着它的边缘流动（或者通过“clear”属性阻止它们这么做）。内容从一个左浮盒的右边往下或者从一个右浮盒的左边往下流动。下面是对浮动定位方式盒内容流动的介绍；“float”属性的描述给出了精确的控制浮动行为的规则。

一个浮动盒被变换到左边或者右边知道它的外边缘接触到包含盒的边缘或者他的外边缘接触到另外一个浮动元素。如果在一个line box中，浮动盒的外顶部和当前line box的顶部对齐。

如果没有足够的水平空间容纳浮动元素，它会往下直到有合适的空间或者不再有浮动元素存在。

Since a float is not in the flow, non-positioned block boxes created before and after the float box flow vertically as if the float did not exist. However, the current and subsequent line boxes created next to the float are shortened as necessary to make room for the margin box of the float.

当存在一个垂直位置全部满足下面四个条件时，一个line box和一个浮动元素相邻：
	
1. 在line box顶部上或在line box顶部的下面。（at or below）。
2. 在line box底部上或在line box底部的上面。（at or above）。
3. 在浮动元素margin边缘的顶部的下面。（below）。
4. 在浮动元素margin边缘的底部的上面。（above）。

注意：这里意味着0高度或者负高度的float元素不会缩短line box。

### 9.5.1 定位浮动元素：“float”属性



### 9.5.2 紧邻浮动元素的控制流：“clear”属性




## 9.6 绝对定位



### 9.6.1 固定定位






## 9.7 “display”，“position”，“float”之间的关系
影响盒生成盒布局的这三个属性——“display”，“position”，和“float”——类似下面的描述的方式相互作用：

1. 如果“display”的值为“none”，“position”和“float”属性不会被应用。在这种情况下，这个元素不会生成盒。
2. 否则，如果“position”的值为“absolute”或“fixed”，盒为绝对定位。“float”计算出的值为“none”，而“display”根据下面的表格设置。盒的位置根据“top”，“right”，“bottom”和“left”属性和盒的包含块决定。
3. 否则，如果“float”是除“none”以外的值，盒为浮动的，且“display”根据下面的表格设置。
4. 否则，如果元素是根元素，“display”根据下面的表格设置，除了CSS2.1中没有定义一个规范值的“list-item”，它的计算值可以是“block”或者“list-item”。
5. 否则，剩下的“display”属性值使用指定值。

<table>
  <tr>
    <th>指定值</th>
    <th>计算值</th>
  </tr>
  <tr>
    <td>Inline-table</td>
    <td>Table</td>
  </tr>
  <tr>
    <td>inline,table-row-group, table-column, table-column-group, table-header-group, table-footer-group, table-row, table-cell, table-caption, inline-block</td>
    <td>block</td>
  </tr>
  <tr>
    <td>others</td>
    <td>Same as specified</td>
  </tr>
</table>



## 9.8 正常流normal flow，浮动floats和绝对定位absolute positioning的对比



### 9.8.1 正常流




### 9.8.2 相对定位




### 9.8.3 浮动盒



### 9.8.4 绝对定位




## 9.9 分层描述



### 9.9.1 指定堆的级别：“z-index”属性





## 9.10 文本方向：“direction”和“unicode-bidi”属性

