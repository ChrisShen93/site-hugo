---
title: "JavaScript中交换两个变量值的常见方法及性能比较"
date: 2018-07-28T21:09:03+08:00
draft: true
tags: ["JavaScript"]
categories: ["学习笔记"]
description: "JavaScript中交换两个变量值的常见方法及性能比较。"
keywords: ["JavsScript", "交换变量"]
---

在 JavaScript 中交换两个变量值，一般有以下几种方法：

## 法一

利用一个临时变量

```javascript
function exchange0 (a, b) {
  let tmp = a;
  a = b;
  b = tmp;
}
```

优点：最简单易懂的方式，适用一切情况，性能高。

缺点：需要使用临时变量。

## 法二

通过和差运算

```javascript
function exchange1 (a, b) {
  a += b;
  b = a - b;
  a -= b;
}
```

优点：不需使用临时变量。

缺点：仅适用于数字类型的交换。

### 法三

通过位运算

```javascript
function exchange2 (a, b) {
  a ^= b;
  b ^= a;
  a ^= b;
}
```

优点：利用位运算，速度快。

缺点：仅适用于数字类型的交换。

## 法四

借助对象

```javascript
function exchange3 (a, b) {
  a = {a:b, b:a};
  b = a.b;
  a = a.a;
}
```

优点：适用于所有类型。

## 法五

借助数组

```javascript
function exchange4 (a, b) {
  a = [a, b];
  b = a[0];
  a = a[1];
}

// 下面是简写形式
function exchange5 (a, b) {
  a = [b, b = a][0];
}
```

优点：适用于所有类型。

缺点：性能似乎有些欠缺。

## 法六

利用ES6的解构赋值

```javascript
function exchange6 (a, b) {
  [a, b] = [b, a];
}
```

优点：适用于所有类型。

## 性能对比

测试环境：

> 操作系统：macOS 10.13.6
>
> 内存大小：16GB
>
> NODE版本：v9.11.2

测试用例1：

```javascript
let a = 1;
let b = 2;
```

| 方法      | 执行次数 | 耗时(ms)  |
| --------- | -------- | --------- |
| exchange0 | 1e9      | 840~888   |
| exchange1 | 1e9      | 836~844   |
| exchange2 | 1e9      | 836~846   |
| exchange3 | 1e9      | 840~848   |
| exchange4 | 1e9      | 843~847   |
| exchange5 | 1e9      | 835~849   |
| exchange6 | 1e9      | 7235~7936 |

测试用例2：

```javascript
let c = 'c';
let d = 'd';
```

| 方法      | 执行次数 | 耗时(ms)  |
| --------- | -------- | --------- |
| exchange0 | 1e9      | 822~865   |
| exchange3 | 1e9      | 807~839   |
| exchange4 | 1e9      | 810~869   |
| exchange5 | 1e9      | 808~841   |
| exchange6 | 1e9      | 7120~7508 |





