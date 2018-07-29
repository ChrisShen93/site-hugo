---
title: "SVG 入门教程"
author: "ChrisShen93"
date: 2018-07-18T15:43:48+08:00
cover: "/img/cover.jpg"
tags: ["note", "svg"]
categories: ["学习笔记"]
description: "SVG 的个人入门教程"
keywords: ["SVG"]
---

# SVG 学习笔记

## 1. 一个最简单的例子

```xml
<svg version="1.1"
     baseProfile="full"
     width="300"
     height="200"
     xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="red"/>
</svg>
```

其中，xmlns必不可少。SVG是XML的一种方言，其命名空间由xmlns指定。

## 2. 理解 viewport，viewBox，preserveAspectRatio

### viewport

即 SVG 可见区域（画布）的大小。

```xml
<svg width="200"
     height="200"
     viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg"
></svg>
```

上面的代码定义了一个视区，宽300单位，高200单位。

width、height可以使用常见的CSS单位，包括em、px、px、pt、pc、cm等。

---

### viewBox

```xml
<svg width="400"
     height="300"
     viewBox="0, 0, 40, 30"
     style="border: 1px solid #cd0000;"
     >
    <rect x="10"
          y="5"
          width="20"
          height="15"
          fill="#cd0000"/>
</svg>
```

<svg width="400" height="300" viewBox="0, 0, 40, 30" style="border: 1px solid #cd0000;" > <rect x="10" y="5" width="20" height="15" fill="#cd0000"/></svg>

（图一）

<svg width="400" height="300" style="border: 1px solid #cd0000;" > <rect x="10" y="5" width="20" height="15" fill="#cd0000"/></svg>

（图二）

按道理，SVG 画布大小为 400 * 300，而rect大小只有 40 * 30，仅为 1/400（见上图二），但实际看起来却是 1/4（见上图一）。之所以有这个差距，就是因为设置了 viewBox。

viewBox 属性里需要设置四个值，分别是 左上角横坐标、左上角纵坐标、宽度、高度。

viewBox 的作用为设置可视区，即用 **选中的可视区** 去铺满 **整个SVG画布**。

---

### preserveAspectRatio

preserveAspectRatio 属性作用于 viewBox，其值有两部分，先举个例子：

```xml
<svg width="400"
     height="200"
     viewBox="0, 0, 200, 200"
     preserveAspectRatio="xMinYMin meet"
     style="border: 1px solid #cd0000;"
     >
    <rect x="10"
          y="10"
          width="150"
          height="150"
          fill="#cd0000"/>
</svg>
```

<svg width="400" height="200" viewBox="0, 0, 200, 200" preserveAspectRatio="xMinYMin meet" style="border: 1px solid #cd0000;" > <rect x="10" y="10" width="150" height="150" fill="#cd0000"/> </svg>

preserveAspectRatio 值的第一部分可以如下取值：

| 值   | 含义                              |
| ---- | --------------------------------- |
| xMin | viewPort 和 viewBox 左边对齐      |
| xMid | viewPort 和 viewBox x轴中心对齐   |
| xMax | viewPort 和 viewBox 右边对齐      |
| YMin | viewPort 和 viewBox 上边缘对齐    |
| YMid | viewPort 和 viewBox y轴中心点对齐 |
| YMax | viewPort 和 viewBox 下边缘对齐    |

preserveAspectRatio 值的第二部分可以如下取值：

| 值    | 含义                                        |
| ----- | ------------------------------------------- |
| meet  | 保持纵横比缩放 viewBox 适应 viewport        |
| slice | 保持纵横比同时比例小的方向放大填满 viewport |
| none  | 扭曲纵横比充分适应 viewport                 |

## 3. 基本形状示例

<svg width="200" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg"> <rect x="10" y="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/> <rect x="60" y="10" rx="10" ry="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/> <circle cx="25" cy="75" r="20" stroke="red" fill="transparent" stroke-width="5"/> <ellipse cx="75" cy="75" rx="20" ry="5" stroke="red" fill="transparent" stroke-width="5"/> <line x1="10" x2="50" y1="110" y2="150" stroke="orange" fill="transparent" stroke-width="5"/> <polyline points="60 110 65 120 70 115 75 130 80 125 85 140 90 135 95 150 100 145" stroke="orange" fill="transparent" stroke-width="5"/> <polygon points="50 160 55 180 70 180 60 190 65 205 50 195 35 205 40 190 30 180 45 180" stroke="green" fill="transparent" stroke-width="5"/> <path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/> </svg>

上述图形对应代码：

```xml
<?xml version="1.0" standalone="no"?>
<svg width="200" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <rect x="10" y="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>
  <rect x="60" y="10" rx="10" ry="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>

  <circle cx="25" cy="75" r="20" stroke="red" fill="transparent" stroke-width="5"/>
  <ellipse cx="75" cy="75" rx="20" ry="5" stroke="red" fill="transparent" stroke-width="5"/>

  <line x1="10" x2="50" y1="110" y2="150" stroke="orange" fill="transparent" stroke-width="5"/>
  <polyline points="60 110 65 120 70 115 75 130 80 125 85 140 90 135 95 150 100 145"
      stroke="orange" fill="transparent" stroke-width="5"/>

  <polygon points="50 160 55 180 70 180 60 190 65 205 50 195 35 205 40 190 30 180 45 180"
      stroke="green" fill="transparent" stroke-width="5"/>

  <path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/>
</svg>
```

## 4. 路径

*path* 是 SVG 中最强大也是最常见的形状。开发者可以通过 path 绘制所有的基本形状、贝塞尔曲线等。

在绘制平滑线条（如曲线）时，path 几乎是唯一的选择。虽然 polyline 也可以实现类似的效果，但是需要设置大量的点，且一旦放大，就能看到明显的离散效果。

path 的形状通过属性 *d* 来定义，其值是一个 **命令 + 参数** 的序列。

### 直线命令

#### M/m 命令

M/m 命令表示 *move to*，大小写的区别是，大写 M 为 **绝对定位**，小写 m 为 **相对定位**。

M/m 命令并不会画线，仅仅是移动画笔，因此一半出现在路径的 **开始处**，来指明从何处开始画。

```
M x y
m dx dy
```

#### L/l 命令

L/l 命令是最简单的画直线命令。与 M/m 相似，大写 L 为 **绝对定位**，小写 l 为 **相对定位**。

L/l 命令的作用是在 *当前位置* 和 *新的位置*（即L/l前画笔所在坐标）直线画一条线段。

```
L x y
l dx dy
```

#### H/h 命令 和 V/v 命令

H/h 命令用来画平行线，V/v 命令用来画垂直线。

```
H x

h dx

V y

v dy
```

#### Z/z 命令

Z/z 命令是一个快捷命令，用来从当前点向起点绘制一条线条，来闭合图形。

Z/z 命令不区分大小写，其效果是相通的。

---

### 曲线命令

#### 贝塞尔曲线

SVG 中有两个命令来绘制贝塞尔曲线：Q/q 命令 和 C/c 命令，分别对应 二次贝塞尔曲线 和 三次贝塞尔曲线。

三次贝塞尔曲线：

格式：(x1, y1) (x2, y2) 分别为两个控制点，(x, y) 为曲线终点。

```
C x1 y1, x2 y2, x y
c dx1 dy1, dx2 dy2, dx dy
```

<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg"> <path d="M10 10 C 20 20, 40 20, 50 10" stroke="black" fill="transparent"/> <circle cx="10" cy="10" r="2" fill="red"/> <circle cx="20" cy="20" r="2" fill="red"/> <path d="M10 10, L20 20" stroke="red"/> <circle cx="40" cy="20" r="2" fill="red"/> <circle cx="50" cy="10" r="2" fill="red"/> <path d="M40 20, L50 10" stroke="red"/> <path d="M70 10 C 70 20, 120 20, 120 10" stroke="black" fill="transparent"/> <circle cx="70" cy="10" r="2" fill="red"/> <circle cx="70" cy="20" r="2" fill="red"/> <path d="M70 10, L70 20" stroke="red"/> <circle cx="120" cy="20" r="2" fill="red"/> <circle cx="120" cy="10" r="2" fill="red"/> <path d="M120 20, L120 10" stroke="red"/> <path d="M130 10 C 120 20, 180 20, 170 10" stroke="black" fill="transparent"/> <circle cx="130" cy="10" r="2" fill="red"/> <circle cx="120" cy="20" r="2" fill="red"/> <path d="M130 10, L120 20" stroke="red"/> <circle cx="180" cy="20" r="2" fill="red"/> <circle cx="170" cy="10" r="2" fill="red"/> <path d="M180 20, L170 10" stroke="red"/> <path d="M10 60 C 20 80, 40 80, 50 60" stroke="black" fill="transparent"/> <circle cx="10" cy="60" r="2" fill="red"/> <circle cx="20" cy="80" r="2" fill="red"/> <path d="M10 60, L20 80" stroke="red"/> <circle cx="40" cy="80" r="2" fill="red"/> <circle cx="50" cy="60" r="2" fill="red"/> <path d="M40 80, L50 60" stroke="red"/> <path d="M70 60 C 70 80, 110 80, 110 60" stroke="black" fill="transparent"/> <circle cx="70" cy="60" r="2" fill="red"/> <circle cx="70" cy="80" r="2" fill="red"/> <path d="M70 60, L70 80" stroke="red"/> <circle cx="110" cy="80" r="2" fill="red"/> <circle cx="110" cy="60" r="2" fill="red"/> <path d="M110 80, L110 60" stroke="red"/> <path d="M130 60 C 120 80, 180 80, 170 60" stroke="black" fill="transparent"/> <circle cx="130" cy="60" r="2" fill="red"/> <circle cx="120" cy="80" r="2" fill="red"/> <path d="M130 60, L120 80" stroke="red"/> <circle cx="180" cy="80" r="2" fill="red"/> <circle cx="170" cy="60" r="2" fill="red"/> <path d="M180 80, L170 60" stroke="red"/> <path d="M10 110 C 20 140, 40 140, 50 110" stroke="black" fill="transparent"/> <circle cx="10" cy="110" r="2" fill="red"/> <circle cx="20" cy="140" r="2" fill="red"/> <path d="M10 110, L20 140" stroke="red"/> <circle cx="40" cy="140" r="2" fill="red"/> <circle cx="50" cy="110" r="2" fill="red"/> <path d="M40 140, L50 110" stroke="red"/> <path d="M70 110 C 70 140, 110 140, 110 110" stroke="black" fill="transparent"/> <circle cx="70" cy="110" r="2" fill="red"/> <circle cx="70" cy="140" r="2" fill="red"/> <path d="M70 110, L70 140" stroke="red"/> <circle cx="110" cy="140" r="2" fill="red"/> <circle cx="110" cy="110" r="2" fill="red"/> <path d="M110 140, L110 110" stroke="red"/> <path d="M130 110 C 120 140, 180 140, 170 110" stroke="black" fill="transparent"/> <circle cx="130" cy="110" r="2" fill="red"/> <circle cx="120" cy="140" r="2" fill="red"/> <path d="M130 110, L120 140" stroke="red"/> <circle cx="180" cy="140" r="2" fill="red"/> <circle cx="170" cy="110" r="2" fill="red"/> <path d="M180 140, L170 110" stroke="red"/> </svg>

```xml
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 10 C 20 20, 40 20, 50 10" stroke="black" fill="transparent"/>
  <circle cx="10" cy="10" r="2" fill="red"/>
  <circle cx="20" cy="20" r="2" fill="red"/>
  <path d="M10 10, L20 20" stroke="red"/>
  <circle cx="40" cy="20" r="2" fill="red"/>
  <circle cx="50" cy="10" r="2" fill="red"/>
  <path d="M40 20, L50 10" stroke="red"/>
  <path d="M70 10 C 70 20, 120 20, 120 10" stroke="black" fill="transparent"/>
  <circle cx="70" cy="10" r="2" fill="red"/>
  <circle cx="70" cy="20" r="2" fill="red"/>
  <path d="M70 10, L70 20" stroke="red"/>
  <circle cx="120" cy="20" r="2" fill="red"/>
  <circle cx="120" cy="10" r="2" fill="red"/>
  <path d="M120 20, L120 10" stroke="red"/>
  <path d="M130 10 C 120 20, 180 20, 170 10" stroke="black" fill="transparent"/>
  <circle cx="130" cy="10" r="2" fill="red"/>
  <circle cx="120" cy="20" r="2" fill="red"/>
  <path d="M130 10, L120 20" stroke="red"/>
  <circle cx="180" cy="20" r="2" fill="red"/>
  <circle cx="170" cy="10" r="2" fill="red"/>
  <path d="M180 20, L170 10" stroke="red"/>
  <path d="M10 60 C 20 80, 40 80, 50 60" stroke="black" fill="transparent"/>
  <circle cx="10" cy="60" r="2" fill="red"/>
  <circle cx="20" cy="80" r="2" fill="red"/>
  <path d="M10 60, L20 80" stroke="red"/>
  <circle cx="40" cy="80" r="2" fill="red"/>
  <circle cx="50" cy="60" r="2" fill="red"/>
  <path d="M40 80, L50 60" stroke="red"/>
  <path d="M70 60 C 70 80, 110 80, 110 60" stroke="black" fill="transparent"/>
  <circle cx="70" cy="60" r="2" fill="red"/>
  <circle cx="70" cy="80" r="2" fill="red"/>
  <path d="M70 60, L70 80" stroke="red"/>
  <circle cx="110" cy="80" r="2" fill="red"/>
  <circle cx="110" cy="60" r="2" fill="red"/>
  <path d="M110 80, L110 60" stroke="red"/>
  <path d="M130 60 C 120 80, 180 80, 170 60" stroke="black" fill="transparent"/>
  <circle cx="130" cy="60" r="2" fill="red"/>
  <circle cx="120" cy="80" r="2" fill="red"/>
  <path d="M130 60, L120 80" stroke="red"/>
  <circle cx="180" cy="80" r="2" fill="red"/>
  <circle cx="170" cy="60" r="2" fill="red"/>
  <path d="M180 80, L170 60" stroke="red"/>
  <path d="M10 110 C 20 140, 40 140, 50 110" stroke="black" fill="transparent"/>
  <circle cx="10" cy="110" r="2" fill="red"/>
  <circle cx="20" cy="140" r="2" fill="red"/>
  <path d="M10 110, L20 140" stroke="red"/>
  <circle cx="40" cy="140" r="2" fill="red"/>
  <circle cx="50" cy="110" r="2" fill="red"/>
  <path d="M40 140, L50 110" stroke="red"/>
  <path d="M70 110 C 70 140, 110 140, 110 110" stroke="black" fill="transparent"/>
  <circle cx="70" cy="110" r="2" fill="red"/>
  <circle cx="70" cy="140" r="2" fill="red"/>
  <path d="M70 110, L70 140" stroke="red"/>
  <circle cx="110" cy="140" r="2" fill="red"/>
  <circle cx="110" cy="110" r="2" fill="red"/>
  <path d="M110 140, L110 110" stroke="red"/>
  <path d="M130 110 C 120 140, 180 140, 170 110" stroke="black" fill="transparent"/>
  <circle cx="130" cy="110" r="2" fill="red"/>
  <circle cx="120" cy="140" r="2" fill="red"/>
  <path d="M130 110, L120 140" stroke="red"/>
  <circle cx="180" cy="140" r="2" fill="red"/>
  <circle cx="170" cy="110" r="2" fill="red"/>
  <path d="M180 140, L170 110" stroke="red"/>
</svg>
```

多条三次贝塞尔曲线连起来，可以绘制为一条很长的平滑曲线。对于三次贝塞尔曲线，如果一个点两侧的控制点对称（斜率一致），则可以使用 **S/s** 命令简写。

格式：

```
S x2 y2, x y
s dx2 dy2, dx dy
```

若 S/s 命令前有 C/c 命令或另一个 S/s 命令，则其第一个控制点会被置为前一个控制点的对称点；若 S/s 命令单独使用，则其两个控制点会被认为是同一个点。

<svg  width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg"> <path d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80" stroke="black" fill="transparent"/> <circle cx="10" cy="80" r="2" fill="red"/> <circle cx="40" cy="10" r="2" fill="red"/> <path d="M10 80, L40 10" stroke="red"/> <circle cx="65" cy="10" r="2" fill="red"/> <circle cx="95" cy="80" r="2" fill="red"/> <path d="M65 10, L95 80" stroke="red"/>   <circle cx="95" cy="80" r="2" fill="red"/> <circle cx="125" cy="150" r="2" fill="blue"/> <path d="M95 80, L125 150" stroke="blue"/> <circle cx="150" cy="150" r="2" fill="red"/> <circle cx="180" cy="80" r="2" fill="red"/> <path d="M150 150, L180 80" stroke="red"/> </svg>

```xml
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80" stroke="black" fill="transparent"/>
  <circle cx="10" cy="80" r="2" fill="red"/>
  <circle cx="40" cy="10" r="2" fill="red"/>
  <path d="M10 80, L40 10" stroke="red"/>
  <circle cx="65" cy="10" r="2" fill="red"/>
  <circle cx="95" cy="80" r="2" fill="red"/>
  <path d="M65 10, L95 80" stroke="red"/>
  <circle cx="95" cy="80" r="2" fill="red"/>
  <circle cx="125" cy="150" r="2" fill="blue"/>
  <path d="M95 80, L125 150" stroke="blue"/>
  <circle cx="150" cy="150" r="2" fill="red"/>
  <circle cx="180" cy="80" r="2" fill="red"/>
  <path d="M150 150, L180 80" stroke="red"/>
</svg>
```

---

二次贝塞尔曲线：

格式：

```
Q x1 y1, x y
q dx1 dy1, dx dy
```

<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg""> <path d="M10 80 Q 95 10 180 80" stroke="black" fill="transparent"/> <circle cx="10" cy="80" r="2" fill="red"/> <circle cx="95" cy="10" r="2" fill="red"/> <circle cx="180" cy="80" r="2" fill="red"/> <path d="M10 80, L95 10" stroke="red"/> <path d="M180 80, L95 10" stroke="red"/> </svg>

```xml
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg"">
  <path d="M10 80 Q 95 10 180 80" stroke="black" fill="transparent"/>
  <circle cx="10" cy="80" r="2" fill="red"/>
  <circle cx="95" cy="10" r="2" fill="red"/>
  <circle cx="180" cy="80" r="2" fill="red"/>
  <path d="M10 80, L95 10" stroke="red"/>
  <path d="M180 80, L95 10" stroke="red"/>
</svg>
```

与三次贝塞尔曲线类似，二次贝塞尔曲线也有个针对对称点的简写命令：**T/t**

```
T x y, x y
t dx dy, dx dy
```

<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg"> <path d="M10 80 Q 52.5 10, 95 80 T 180 80" stroke="black" fill="transparent"/> <circle cx="10" cy="80" r="2" fill="red"/> <circle cx="52.5" cy="10" r="2" fill="red"/> <path d="M10 80, L52.5 10" stroke="red"/> <circle cx="95" cy="80" r="2" fill="red"/> <path d="M52.5 10, L95 80" stroke="red"/> <circle cx="137.5" cy="150" r="2" fill="red"/> <path d="M95 80, L137.5 150" stroke="blue"/> <circle cx="180" cy="80" r="2" fill="red"/> <path d="M137.5 150, L180 80" stroke="blue"/> </svg>

```xml
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 Q 52.5 10, 95 80 T 180 80" stroke="black" fill="transparent"/>
  <circle cx="10" cy="80" r="2" fill="red"/>
  <circle cx="52.5" cy="10" r="2" fill="red"/>
  <path d="M10 80, L52.5 10" stroke="red"/>
  <circle cx="95" cy="80" r="2" fill="red"/>
  <path d="M52.5 10, L95 80" stroke="red"/>
  <circle cx="137.5" cy="150" r="2" fill="red"/>
  <path d="M95 80, L137.5 150" stroke="blue"/>
  <circle cx="180" cy="80" r="2" fill="red"/>
  <path d="M137.5 150, L180 80" stroke="blue"/>
</svg>
```

#### 弧形

格式：

```
A rx ry x-axis-rotation large-arc-flag sweep-flag x y
a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy
```

参数说明：

| rx      | ry      | x-axis-rotation             | large-arc-flag                                               | sweep-flag                                                   | x           | y           |
| ------- | ------- | --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- | ----------- |
| x轴半径 | r轴半径 | 弧形的旋转状况，单位为度(°) | 角度大小。0表示小角度弧（小于180°），1表示大角度弧（大于180°） | 弧线方向。0表示从起点到终点逆时针画弧，1表示从起点到终点顺时针画弧。 | 终点x轴坐标 | 终点y轴坐标 |

<svg width="320px" height="320px" version="1.1" xmlns="http://www.w3.org/2000/svg"> <path d="M10 315 L 110 215 A 30 50 0 0 1 162.55 162.45 L 172.55 152.45 A 30 50 -45 0 1 215.1 109.9 L 315 10" stroke="black" fill="green" stroke-width="2" fill-opacity="0.5"/></svg>

```xml
<svg width="320px" height="320px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 315
           L 110 215
           A 30 50 0 0 1 162.55 162.45
           L 172.55 152.45
           A 30 50 -45 0 1 215.1 109.9
           L 315 10" stroke="black" fill="green" stroke-width="2" fill-opacity="0.5"/>
</svg>
```

在确认了rx、ry之后，对于左下方没有旋转的弧，实际上有两种画法（对角线正好经过了椭圆的中心large-arc-flag设置0或者1都一样，因此不是四种）。

<svg width="320px" height="320px" version="1.1" xmlns="http://www.w3.org/2000/svg"> <path d="M10 315 L 110 215 M 162.55 162.45 L 315 10" stroke="black" stroke-width="2"/> <path d="M110 215 A 30 50 0 0 1 162.55 162.45" stroke="red" fill="transparent"></path> <path d="M110 215 A 30 50 0 0 0 162.55 162.45" stroke="blue" fill="transparent"></path> </svg>

```xml
<svg width="320px" height="320px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 315
           L 110 215
           M 162.55 162.45
           L 315 10"
        stroke="black" stroke-width="2"/>
  <path d="M110 215
           A 30 50 0 0 1 162.55 162.45"
        stroke="red" fill="transparent"></path>
  <path d="M110 215
           A 30 50 0 0 0 162.55 162.45"
        stroke="blue" fill="transparent"></path>
</svg>
```

下面的例子展示了完整的由 **large-arc-flag** 和 **sweep-flag** 组成的四种图形

<svg width="325px" height="325px" version="1.1" xmlns="http://www.w3.org/2000/svg"> <circle cx="125" cy="80" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <circle cx="80" cy="125" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <path d="M80 80 A 45 45, 0, 0, 0, 125 125 L 125 80 Z" fill="green" fill-opacity="0.5"/> <text x="45" y="45">large-arc-flag=0</text> <text x="45" y="60">sweep-flag=0</text> <circle cx="275" cy="80" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <circle cx="230" cy="125" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <path d="M230 80 A 45 45, 0, 1, 0, 275 125 L 275 80 Z" fill="red" fill-opacity="0.5"/> <text x="195" y="45">large-arc-flag=1</text> <text x="195" y="60">sweep-flag=0</text> <circle cx="125" cy="230" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <circle cx="80" cy="275" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <path d="M80 230 A 45 45, 0, 0, 1, 125 275 L 125 230 Z" fill="purple" fill-opacity="0.5"/> <text x="45" y="195">large-arc-flag=0</text> <text x="45" y="210">sweep-flag=1</text> <circle cx="275" cy="230" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <circle cx="230" cy="275" r="45" stroke="#ddd" stroke-width="2" fill="transparent"/> <path d="M230 230 A 45 45, 0, 1, 1, 275 275 L 275 230 Z" fill="blue" fill-opacity="0.5"/> <text x="195" y="195">large-arc-flag=1</text> <text x="195" y="210">sweep-flag=1</text> </svg>

```xml
<svg width="325px" height="325px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <circle cx="125"
          cy="80"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <circle cx="80"
          cy="125"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <path d="M80 80
           A 45 45, 0, 0, 0, 125 125
           L 125 80 Z"
        fill="green"
        fill-opacity="0.5"/>
  <text x="45" y="45">large-arc-flag=0</text>
  <text x="45" y="60">sweep-flag=0</text>
  <circle cx="275"
          cy="80"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <circle cx="230"
          cy="125"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <path d="M230 80
           A 45 45, 0, 1, 0, 275 125
           L 275 80 Z"
        fill="red"
        fill-opacity="0.5"/>
  <text x="195" y="45">large-arc-flag=1</text>
  <text x="195" y="60">sweep-flag=0</text>
  <circle cx="125"
          cy="230"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <circle cx="80"
          cy="275"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <path d="M80 230
           A 45 45, 0, 0, 1, 125 275
           L 125 230 Z"
        fill="purple"
        fill-opacity="0.5"/>
  <text x="45" y="195">large-arc-flag=0</text>
  <text x="45" y="210">sweep-flag=1</text>
  <circle cx="275"
          cy="230"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <circle cx="230"
          cy="275"
          r="45"
          stroke="#ddd"
          stroke-width="2"
          fill="transparent"/>
  <path d="M230 230
           A 45 45, 0, 1, 1, 275 275
           L 275 230 Z"
        fill="blue"
        fill-opacity="0.5"/>
  <text x="195" y="195">large-arc-flag=1</text>
  <text x="195" y="210">sweep-flag=1</text>
</svg>
```

## 5. 填充和边框

### 上色

| 属性           | 描述                   | 值                                                           |
| -------------- | ---------------------- | ------------------------------------------------------------ |
| fill           | 对象内部的填充色       | 颜色名（像*red*这种）、rgb值（像rgb(255,0,0)这种）、十六进制值、rgba值，等。 |
| stroke         | 对象的线条色           | 同上                                                         |
| fill-opacity   | 对象内部填充色的透明度 | 0～1。0为透明，1为完全不透明                                 |
| stroke-opacity | 对象线条色的透明度     | 同上                                                         |

### 描边

| 属性              | 描述                                            | 值                                                           |
| ----------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| stroke-width      | 描边的宽度                                      |                                                              |
| stroke-linecap    | 描边终点的形状                                  | butt: 用直线结束线段<br/>square: 用直线结束线段，但是会超出实际路径。超出的宽度由stroke-width确定<br/>round: 用圆角结束线段。圆角的半径由stroke-width确定 |
| stroke-linejoin   | 两条描边之间的连接方式                          | miter:  用方形画笔在连接处形成尖角<br/>round:  用圆角连接，实现平滑效果<br/>bevel:  连接处会形成一个斜接 |
| stroke-dasharray  | 虚线类型应用在描边上                            |                                                              |
| fill-rule         | 定义如何给图形重叠的区域上色                    |                                                              |
| stroke-miterlimit | 定义什么情况下绘制或不绘制边框连接的`miter`效果 |                                                              |
| stroke-dashoffset | 定义虚线开始的位置                              |                                                              |

### 使用CSS

SVG 规范，将 SVG 的属性分为 *properties* 和 *attributes*。对于 **properties**，可以使用CSS达到与内联样式相同的效果；而对于 **attributes** 则不可以。[SVG规范](https://www.w3.org/TR/SVG/propidx.html)

## 6. 渐变

渐变分为线性渐变和径向渐变。渐变内容 **必须** 指定一个 *id* 属性，否则文档内的其他元素就不能引用它。

为了让渐变能被重复使用，渐变内容需要定义在 **&lt;defs&gt;** 标签内部，而不是定义在形状上面。

### 线性渐变

线性渐变沿着直线改变颜色，要插入一个线性渐变，你需要在SVG文件的 `defs元素` 内部，创建一个[&lt;linearGradient&gt;](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/linearGradient) 节点。

<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">  <defs>      <linearGradient id="Gradient1">        <stop class="stop1" offset="0%"/>        <stop class="stop2" offset="50%"/>        <stop class="stop3" offset="100%"/>      </linearGradient>      <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">        <stop offset="0%" stop-color="red"/>        <stop offset="50%" stop-color="black" stop-opacity="0"/>        <stop offset="100%" stop-color="blue"/>      </linearGradient>      <style type="text/css"><![CDATA[        #rect1 { fill: url(#Gradient1); }        .stop1 { stop-color: red; }        .stop2 { stop-color: black; stop-opacity: 0; }        .stop3 { stop-color: blue; }      ]]></style>  </defs>   <rect id="rect1" x="10" y="10" rx="15" ry="15" width="100" height="100"/>  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#Gradient2)"/>  </svg>

<style> #rect1 { fill: url(#Gradient1); } .stop1 { stop-color: red; } .stop2 { stop-color: black; stop-opacity: 0; } .stop3 { stop-color: blue; } </style>

```xml
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <linearGradient id="Gradient1">
        <stop class="stop1" offset="0%"/>
        <stop class="stop2" offset="50%"/>
        <stop class="stop3" offset="100%"/>
      </linearGradient>
      <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="50%" stop-color="black" stop-opacity="0"/>
        <stop offset="100%" stop-color="blue"/>
      </linearGradient>
      <style type="text/css"><![CDATA[
        #rect1 { fill: url(#Gradient1); }
        .stop1 { stop-color: red; }
        .stop2 { stop-color: black; stop-opacity: 0; }
        .stop3 { stop-color: blue; }
      ]]></style>
  </defs>
  <rect id="rect1" x="10" y="10" rx="15" ry="15" width="100" height="100"/>
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#Gradient2)"/>
</svg>
```

> <![CDATA[]]> 中的内容不会被 XML 解析器解析。

&lt;linearGradient&gt; 元素还需要一些其他的属性值，它们指定了渐变的大小和出现范围。渐变的方向可以通过两个点来控制，它们分别是属性x1、x2、y1和y2，这些属性定义了渐变路线走向。渐变色默认是水平方向的，但是通过修改这些属性，就可以旋转该方向。

### 径向渐变

径向渐变与线性渐变相似，只是它是从一个点开始发散绘制渐变。创建径向渐变需要在文档的`defs元素`中添加一个[<radialGradient>](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/radialGradient)元素。

<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">  <defs>      <radialGradient id="RadialGradient1">        <stop offset="0%" stop-color="red"/>        <stop offset="100%" stop-color="blue"/>      </radialGradient>      <radialGradient id="RadialGradient2" cx="0.25" cy="0.25" r="0.25">        <stop offset="0%" stop-color="red"/>        <stop offset="100%" stop-color="blue"/>      </radialGradient>  </defs>   <rect x="10" y="10" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient1)"/>   <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient2)"/>   </svg>

```xml
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <radialGradient id="RadialGradient1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
      <radialGradient id="RadialGradient2" cx="0.25" cy="0.25" r="0.25">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>
 
  <rect x="10" y="10" rx="15" ry="15" width="100" height="100"
        fill="url(#RadialGradient1)"/> 
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100"
        fill="url(#RadialGradient2)"/> 
</svg>
```

&lt;radialGradient&gt; 的几个特殊属性：

| 属性         | 描述                         | 值                      |
| ------------ | ---------------------------- | ----------------------- |
| cx           | 渐变结束所围绕的圆环的中心点 | 数字或百分比，默认为50% |
| cy           | 渐变结束所围绕的圆环的中心点 | 数字或百分比，默认为50% |
| r            | 渐变结束所围绕的圆环的半径   | 默认为50%               |
| fx           | 渐变的焦点                   | 默认为0%                |
| fy           | 渐变的焦点                   | 默认为0%                |
| spreadMethod | 用于描述渐变过程             | pad/refleact/repeat     |



关于渐变，建议了解 **[gradientUnits](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/gradientUnits)**，其值有两个 *userSpaceOnUse* 和 *objectBoundingBox* (默认)。