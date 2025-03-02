---
title: 'R语言可视化学习笔记'
date: 2025-2-3
permalink: /posts/2013/08/blog-post-5/
tags:
  - cool posts
  - category1
  - category2
---

# R语言可视化

## 第一章:R基础

### 1.3加载分隔符式文件(csv文件)

方法:

data &lt;-read.csv("datafile.csv")

注意:

(1)如果文件首行没有列名,则可以用

data &lt;-read.csv("datafile.csv", header=FALSE)#得到的数据框的列名将是 v1、V2

#可以手动为列名赋值

names(data) &lt;-c("Column","Column2""Column3")

#还可以设置分隔符 sep 参数来设置分隔符号。如果是空格分隔,使用 secp="";如果是制表符分隔,使用\t。

data &lt;-read.csv("datafile,csv",5ep="t")

(2)默认情况下,数据集中的字符串 (string)会被视为因子 (factor)处理,可以用

“stringsAsFactors=FALSE”,将因子转换为字符串

### 1.4从excel加载数据

#### 方法:

xlsx 包中的函数 read.xlsx() 可以读取 Excel文件,下面的代码将会读取 Excel中的第一个工作表:

install.packages("xlsx")

library(xslx)

data &lt;-read.xlsx("datafile.xlsx",1)

如果需要阅读老版本的 Excel 文件 (.xls 格式),gdata 包提供了函数 read.xls():

install.packaqes("adata")

library(qdata)

#读取第一张工作表

data &lt;-read.xls("datafile.xls")

注意:

(1)使用 read.xlsx()加载工作表时,既可以用序数参数sheetIndex 来指定,也可以用工作表名参数sheetName 来指定:

data &lt;-read.xlsx("datafile.xs", sheetIndex=)

data &lt;-read.xlsx("datafile.xls",sheetName="Revenues")

(2)使用 read.xls()加载工作表时,可以用序数参数 sheet 来指定:

data &lt;-read.xlsx("datafile.xls",sheet=2)

### 1.5从spss加载文件

方法:

foreign 包中的函数 read.spss() 可以读取 SPSS 文件。若要读取SPSS 文件中的第一张表:

install.packages(foreign”)

library(foreign)

data &lt;-read.spss("datafile.sav")

注意:

foreign 包中还有很多读取其他格式文件的函数,包括以下几种

read.octave():Octave和MATLAB。.

read.systat() :SYSTAT。

read.xport():SAS XPORT

read.dta() :Stata。

## 第二章:快速探索数据

介绍qplot函数

语法

qplot(data,x,y,facets,geom,main,xlab,ylab,asp)

参数意义:

data :需要绘制的数据框

x,y: 用于指定图表中每一层的美学特征

geom: 用于指定要绘制的几何图形。[如果指定了x和Y,则为散点图,如果只指定了X,则为直方图,”boxplot “为箱形图,”violin “为小提琴图等等,] 。

main: 在图上添加标题

xlab , ylab: 用来在绘图的x轴和y轴上添加标签。

shape – 用来定义基于分类属性的对象的形状

color – 用于通过考虑分类属性为数据点着色

size – 用于指定数据点的大小。

### 2.1绘制散点图

### 1.plot函数绘制

plot(x, y, ...)

2.ggplot绘制

plot(x, y, data, geom, main, xlab, ylab, ...)

参数意义:

x : x轴的数据。

y : y轴的数据。

data : 包含数据的数据框。

geom : 用于指定几何对象(图形类型),例如 "point" 表示散点图。

main : 主标题。

xlab : x轴的标签。

ylab : y轴的标签。

... : 其他参数,用于定制图形的外观。

例:

# 创建示例数据

data&lt;-data.frame(

x=c(1,2,3,4,5),

y=c(2,4,6,8,10)

)

# 使用qplot创建散点图

qplot(x=x, y=y, data=data, 9eom="po∈t", main = "Scatterplot",×7ab="x 轴标签",轴标签",y7ab="r轴标签")轴标签")


![](https://web-api.textin.com/ocr_image/external/df91daef41c89f8e.jpg)

2.2绘制折线图

1.使用plot函数

2.使用ggplot2绘制

qplot(x, y, data, geom, main, xlab, ylab, ...)

其中:

x: x轴的数据。

y: y轴的数据。

data: 包含数据的数据框。

geom: 用于指定几何对象(图形类型),例如 "line" 表示折线图

main: 主标题。

xlab: x轴的标签。

ylab: y轴的标签。

例:

# 创建示例数据

data&lt;-data.frame(

x=c(1,2,3,4,5),

y=c(2,4,6,8,10)

)

# 使用qplot创建折线图

qplot(x=x, y=y, data=data, 9eom="7∈e", main="Line Plot", ×7ab="×轴标

签",y7ab="Y轴标签")

### 2.3绘制条形图

#### 1.使用barpot绘制(之前学过)

barplot(height, ...)

### 参数

height 是一个向量,表示每个条形的高度。

... 表示可选参数,用于定制条形图的外观和属性

### 2.使用ggplot2函数

qplot(x, y, data, geom, main, xlab, ylab, ...)

其中:

x : x轴的数据。

y : y轴的数据。

data : 包含数据的数据框。

geom : 用于指定几何对象(图形类型),例如 "bar" 表示条形图

main : 主标题。

xlab : x轴的标签。

ylab : y轴的标签。

stat:设置为identity

... : 其他参数,用于定制图形的外观。

#### 2.4绘制直方图

1.hist函数绘制

hist(x,⋯)

参数:

x 是包含数据的向量或数值变量。

... 表示可选参数,用于定制直方图的外观和属性。

### 2.qplot绘制

qplot(x, data, geom = "histogram", bins=⋯, main=⋯,×1ab=⋯,y1ab=...)

参数:

x 是包含数据的向量或数值变量。

data 是包含数据的数据框。

geom 用于指定几何对象,这里设为 "histogram" 表示绘制直方图。

bins 表示直方图的分箱数目。

main、xlab、ylab 分别用于设置主标题、x轴标签和y轴标签。

### 2.5绘制箱线图(必须是因子型变量)

1.plot绘制

使用plot()函数绘制箱线图时向其传递两个向量:x和y,当x为因子型变量(与数值型变量对应) 时,它会默认绘制箱线图:

plot(ToothGrowth&#36;supp,ToothGrowth&#36;len)

当两个参数向量包含在同一个数据框中时,也可以使用公式语法。公式语法允许我们在x轴上使用变量组合,如

#公式语法

boxplot(len \~ supo,data = ToothGrowth)

#在X轴上引入两变量的交互

boxplot(len∼supp+dose, data=ToothGrowth)

### 2.qplot绘制

qplot(x,y, data,$geom="bo\times plot^{\prime \prime }$, main, xlab, ylab, ...)

参数:

x 是箱线图中的 x 轴变量,通常是类别型变量。

y 是箱线图中的 y 轴变量,通常是数值型变量

data 是包含数据的数据框

$9eom="bo\times plot^{\prime \prime }$用于指定绘制箱线图

注意:

(1)当两个参数向量在同一个数据框内时,则可以使用下面的语句:

qplot(supp,len,data=ToothGrowth,geom="boxplot")

(2)使用interaction()函数将分组变量组合在一起也可以绘制基于多分组变量的箱线图

#使用三个独立的向量参数

gplot(interaction(ToothGrowthSsupp,ToothGrowthsdose),

ToothGrowthslen,geom="boxplot")

#也可以以数据框中的列作为参数qplot(interaction(supp,dose),len,data=ToothGrowth,$9eom="bo\times plot^{\prime \prime })$

2.6绘制函数图像

1.curve绘制

使用时需向其传递一个关于变量x的表达式:

$curve(x\wedge 3-5^{*}x,from=-4,$ to=4)

你可以绘制任何一个以数值型向量作为输入且以数值型向量作为输出的函数图像,包括你自己定义的函数

curve(expr,from=min,to=max, cot1=⋯, 1wd=⋯,n=⋯, add=FALSE,...)

参数意义:

expr 是一个包含要绘制的函数的表达式。

from 和 to 是 x 轴的范围。

col 是曲线的颜色

lwd 是曲线的宽度

n 是用于生成曲线的点的数量

add 是一个逻辑值,表示是否将曲线添加到已有的图形上

例:

curve(x∧2,from=-2,to=2, col="blue",, 1wd=2, main = "Function Plot", xlab ="×轴,y7ab="Y轴")


![](https://web-api.textin.com/ocr_image/external/936938045143fb88.jpg)

### 2.使用ggplot2绘制函数

使用时需设定stat="function"和geom="l∈e",并向其传递一个输入和输出皆为数值型向量的函数

library(ggplot2)

#将x轴的取值范围设定为0到20

myfun&lt;-function(x)x∧3

data &lt;- data.frame(x=c(0, 20))

ggplot(data, aes (x=x))+5tanction(fun=myfun, $geom=^{\prime \prime }1\in e^{\prime \prime })$

#用qplot绘制


![](https://web-api.textin.com/ocr_image/external/efe097851162cedd.jpg)
