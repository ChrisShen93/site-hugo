---
title: "JS 取文件的 MIME type 为空字符串"
date: 2018-11-28T16:52:34+08:00
keywords: ["MIME type", "JavaScript"]
description: "JS 取文件的 MIME type 为空字符串"
---

今天被提到一个bug：系统中无法上传zip文件和rar文件。

查了一下代码，无法上传zip文件是因为在 `input[type=file]` 的 `accept` 属性中漏了一条 `application/x-zip-compressed`。

而 rar 的问题出在，`file.type` 取出的值为空字符串。

```javascript
const fileMime = file.type
console.log(fileMime === '') // true
```

经过一番查阅，原因锁定在 `文件嗅探算法(File Sniffing Algorithm)`。

该算法的具体描述可见：[whatwg](https://mimesniff.spec.whatwg.org/)

这套 嗅探算法 的核心在于 `字节模式匹配(byte pattern matching)`。

对于一个 *WinRAR* 文件来说，只有匹配到 **52 61 72 20 1A 07 00** 这一特殊的字节模式，`file.type` 才会返回 `application/x-rar-compressed`，而在我的例子中，却是 **52 61 72 21 1A 07 00**，所以按照文件嗅探算法的规范，返回了一个空字符串。

## 疑惑

在我的场景中，打开文件选择框，是可以看见rar格式文件的。无法上传rar文件实际上是在我发送ajax之前对文件类型又进行了一次判断，这一次没有取到想要的 MIME type。

## 总结

对于有文件类型验证的前端需求，可以考虑 MIME type + extension name 的方式，而不是单纯地相信浏览器的 嗅探。

推荐一个js库：[mimetype-js](https://github.com/rsdoiel/mimetype-js)
