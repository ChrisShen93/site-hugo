---
title: "在 Vue 中使用 JSX 的一些注意事项"
date: 2018-07-25T08:57:10+08:00
tag: ["Vue", "JSX"]
description: "在 Vue 中使用 JSX 的一些注意事项"
keywords: ["Vue", "JSX"]
---

## 使用 JSX

Vue 的 template 书写起来很方便，但是对于 **Vue 2.5.0** 之前的版本来说，想使用 `functional(stateless) 组件`，就需要放弃使用 template，而去使用 `render` 方法（）。

```html
<template>
  <div>
    {{ msg }}
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'hello'
    }
  }
 }
</script>
```

上面这段在 vue-loader 处理之后的结果是：

```js
export default {
  data () {
    return {
      msg: 'hello'
    }
  },
  render () {
    var _vm = this;
    var _h = _vm.$createElement;
    var _c = _vm._self_.c || _h;
    return _c('div', [
      _vm._v(_vm._s(_vm.msg)),
      _c('div')
    ])
  }
}
```

此处的 **`createElement`** 函数即平时所说的 **`h`** 函数，Vue 用它来创建一个 VNode。同时，`createElement` 也是 `render` 函数的第一个参数。

在 render 中写 JSX：

```jsx
export default {
  data () {
    return {
      msg: 'hello'
    }
  },
  render () {
    return (
      <div>{ this.msg }</div>
    )
  }
}
```

会被转换成：

```js
export default {
  data () {
    return {
      msg: 'hello'
    }
  },
  render () {
    const h = arguments[0]
    return h(
    	'div',
      null,
      [this.msg]
    )
  }
}
```

> 在 render 中可以直接使用 createElement 方法。但是如果需要使用 JSX 语法的话，则需要加入 `babel-plugin-transform-vue-jsx`、`babel-plugin-syntax-jsx`、`babel-helper-vue-jsx-merge-props`、`babel-preset-env`，这四个 babel 插件。

## 在 JSX 中使用 template scope (scopedSlots)

在 **&lt;template/&gt;** 使用 template scope(从2.5.0开始是scopedSlots)，是一件很轻松又随意的事情：

```xml
<!-- version < 2.5.0 -->
<my-components>
  <template scope="scope"></template>
</my-components>

<!-- version >= 2.5.0 -->
<my-components>
  <template slot-scope="scope"></template>
</my-components>
```

而在 JSX 中使用，就稍微麻烦一些：

```jsx
export default {
  render () {
    return (
      <my-components scopedSlots={
        {
          default: function (scope) {
            return [<div>{ scope.text }</div>, <div>This is the real body</div>]
          }
        }
      }/>
    )
  }
}

// 如果是 default scope，那么也可以直接简写
export default {
  render () {
    return (
      <my-components>
      {
        scope => (
          <div>
            { scope.text }
          </div>
        )
      }
      </my-components>
    )
  }
}
```

