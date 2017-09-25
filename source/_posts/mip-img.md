---
title: mip-img 图片使用
desc: mip-img 用来支持在 mip 中增加图片内容。
---

> 摘自 [MIP官网 - mip-img 图片](https://www.mipengine.org/examples/mip/mip-img.html)

mip-img 用来支持在 mip 中增加图片内容。

标题 | 内容
--- | ---
类型 | 通用
支持布局 | `responsive, fixed-height, fill, container, fixed`
所需脚本 | 无

<!-- more -->

## 示例

<div class="tip-info">
注意： <code>&lt;mip-img&gt;</code> 需要对应闭合标签 <code>&lt;/mip-img&gt;</code> , 不支持自闭合写法。自闭合规范请见 <a href="https://www.w3.org/TR/html/syntax.html#void-elements">w3.org</a>。
</div>

<img src="/images/300x300.png" width="300" height="300" alt="mip-img demo">

### 最基本使用

```html
<mip-img
    layout="responsive"
    width="350"
    height="263"
    src="https://www.mipengine.org/static/img/sample_01.jpg">
</mip-img>
```

### 加全屏查看

```html
<mip-img
    layout="responsive"
    width="350"
    height="263"
    popup
    src="https://www.mipengine.org/static/img/sample_01.jpg">
</mip-img>
```

### 其他布局（以fixed为例）

```html
<mip-img
    layout="fixed-height"
    height="263"
    alt="baidu mip img"
    src="https://www.mipengine.org/static/img/sample_01.jpg">
</mip-img>
```

### 带图片标题

图片标题可添加在 `<mip-img>` 后用于说明，可在 `<style mip-custom>` 标签下自定义样式

```html
<mip-img
    layout="responsive"
    width="350"
    height="263"
    popup
    alt="baidu mip img"
    src="https://www.mipengine.org/static/img/sample_01.jpg">
</mip-img>
<p class="mip-img-subtitle">带图片标题的类型</p>
```
