---
slug: grid布局
title: grid布局
authors:
  name: Kevin
  title: grid布局
  url: https://github.com/timspan
  image_url: https://timspan.gitee.io/creative_website/assets/dog.e73586b8.jpg
tags: [hola, docusaurus]
---




# grid布局

![img](https://www.wangbase.com/blogimg/asset/201903/1_bg2019032502.png)

容器里面的水平区域称为"行"（row），垂直区域称为"列"（column）。

行和列的交叉区域，称为"单元格"（cell）。

![img](https://www.wangbase.com/blogimg/asset/201903/1_bg2019032503.png)

划分网格的线，称为"网格线"（grid line）

## 1_容器属性

### display 属性

`display: grid`指定一个容器采用网格布局。

```css
div {
  display: grid;
}
```



![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032504.png)



默认情况下，容器元素都是块级元素，但也可以设成行内元素

```css
div {
  display: inline-grid;
}
```





:::tip 注意

设为网格布局以后，容器子元素（项目）的`float`、`display: inline-block`、`display: table-cell`、`vertical-align`和`column-*`等设置都将失效。

:::



## grid-template-columns  和 grid-template-rows 属性

`grid-template-columns`属性定义每一列的列宽，`grid-template-rows`属性定义每一行的行高。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
```



![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032506.png)

指定了一个三行三列的网格，列宽和行高都是`100px`

除了使用绝对单位，也可以使用百分比。

```css
.container {
  display: grid;
  grid-template-columns: 33.33% 33.33% 33.33%;
  grid-template-rows: 33.33% 33.33% 33.33%;
}
```

### repeat()重复

可以使用`repeat()`函数，简化重复的值。上面的代码用`repeat()`改写如下。

```css

.container {
  display: grid;
  grid-template-columns: repeat(3, 33.33%);
  grid-template-rows: repeat(3, 33.33%);
}
// repeat()接受两个参数，第一个参数是重复的次数（上例是3），第二个参数是所要重复的值。
```



```css
grid-template-columns: repeat(2, 100px 20px 80px);
```

定义了6列，第一列和第四列的宽度为`100px`，第二列和第五列为`20px`，第三列和第六列为`80px`。



![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032507.png)



### auto-fill 自动填充

有时，单元格的大小是固定的，但是容器的大小不确定。如果希望每一行（或每一列）容纳尽可能多的单元格，这时可以使用`auto-fill`关键字表示自动填充

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

表示每列宽度`100px`，然后自动填充，直到容器不能放置更多的列。



![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032508.png)



### fr片段-fraction缩写

表示比例关系.如果两列的宽度分别为`1fr`和`2fr`，就表示后者是前者的两倍。

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```

表示两个相同宽度的列。



![img](https://www.wangbase.com/blogimg/asset/201903/1_bg2019032509.png)

:::tip 注意

`fr`可以与绝对长度的单位结合使用，这时会非常方便。

::: 

```css
.container {
  display: grid;
  grid-template-columns: 150px 1fr 2fr;
}
```





![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032510.png)

### minmax()

`minmax()`函数产生一个长度范围，表示长度就在这个范围之中。它接受两个参数，分别为最小值和最大值。

> ```css
> grid-template-columns: 1fr 1fr minmax(100px, 1fr);
> ```

上面代码中，`minmax(100px, 1fr)`表示列宽不小于`100px`，不大于`1fr`。

### auto 关键字

`auto`关键字表示由浏览器自己决定长度。

> ```css
> grid-template-columns: 100px auto 100px;
> ```

上面代码中，第二列的宽度，基本上等于该列单元格的最大宽度，除非单元格内容设置了`min-width`，且这个值大于最大宽度。

### 网格线的名称

`grid-template-columns`属性和`grid-template-rows`属性里面，还可以使用方括号，指定每一根网格线的名字，方便以后的引用。

> ```css
> .container {
>   display: grid;
>   grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
>   grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
> }
> ```

上面代码指定网格布局为3行 x 3列，因此有4根垂直网格线和4根水平网格线。方括号里面依次是这八根线的名字。

## grid-row-gap 和grid-column

`grid-row-gap`属性设置行与行的间隔（行间距），`grid-column-gap`属性设置列与列的间隔（列间距）。

```css
.container {
  grid-row-gap: 20px;
  grid-column-gap: 20px;
}
```



![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032511.png)

###  grid-gap 合并写法



### grid-template-areas 属性

grid-au划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。默认的放置顺序是"先行后列"，即先填满第一行，再开始放入第二行，即下图数字的顺序。o-flow 属性

这个顺序由`grid-auto-flow`属性决定，默认值是`row`，即"先行后列"。也可以将它设成`column`，变成"先列后行"。

## justify-items 和 align-items 和 place-items 属性

justify:左-中-右对齐

align:上-中-下对齐

`justify-items`属性设置单元格内容的水平位置（左中右），`align-items`属性设置单元格内容的垂直位置（上中下）。

stretch：拉伸，占满单元格的整个宽度（默认值）

:::tip 值 注意:是**设置单元格内容**

- start：对齐单元格的起始边缘。
- end：对齐单元格的结束边缘。
- center：单元格内部居中。
- stretch：拉伸，占满单元格的整个宽度（默认值）。

:::

## justify-content 和align-content 和 place-content 属性

:::tip 注意:是**设置整个内容区域**

`justify-content`属性是整个内容区域在容器里面的水平位置（左中右），`align-content`属性是整个内容区域的垂直位置（上中下）。

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```

:::

## grid-auto-columns 和grid-auto-rows 属性

## grid-template 和 grid 属性-简写形式

`grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式。

`grid`属性是`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、 `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式。

## 2_项目属性

### grid-column-start 和 grid-column-end 和grid-row-start 和 grid-row-end 属性

项目的位置是可以指定的，具体方法就是指定项目的四个边框，分别定位在哪根网格线。

- `grid-column-start`属性：左边框所在的垂直网格线
- `grid-column-end`属性：右边框所在的垂直网格线
- `grid-row-start`属性：上边框所在的水平网格线
- `grid-row-end`属性：下边框所在的水平网格线

```css
.item-1 {
  grid-column-start: 2;
  grid-column-end: 4;
}
```

1号项目的左边框是第二根垂直网格线，右边框是第四根垂直网格线。

![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032526.png)



### grid-column和 grid-row 属性-简写形式

`grid-column`属性是`grid-column-start`和`grid-column-end`的合并简写形式，`grid-row`属性是`grid-row-start`属性和`grid-row-end`的合并简写形式。

### justify-self 和 align-self 和 place-self 属性

`justify-self`属性设置单元格内容的水平位置（左中右），跟`justify-items`属性的用法完全一致，但只作用于单个项目。

`align-self`属性设置单元格内容的垂直位置（上中下），跟`align-items`属性的用法完全一致，也是只作用于单个项目。

### 上述只作用于单个项目

这两个属性都可以取下面四个值。

- start：对齐单元格的起始边缘。
- end：对齐单元格的结束边缘。
- center：单元格内部居中。
- stretch：拉伸，占满单元格的整个宽度（默认值）。

```css
.item-1  {
  justify-self: start;
}
```



![img](https://www.wangbase.com/blogimg/asset/201903/bg2019032532.png)















