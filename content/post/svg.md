---
title: "SVG"
author: "ChrisShen93"
date: 2018-07-18T15:43:48+08:00
cover: "/img/cover.jpg"
tags: ["note", "svg"]
categories: ["学习笔记"]
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

---

---

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

