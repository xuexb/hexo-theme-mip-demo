---
title: 为 Hexo 制作 MIP 主题
desc: 关于 Hexo MIP 模板
---

前两天看了下 [Hexo](https://hexo.io/) ，第一眼望去，感觉略复杂啊。在主题市场搜一些 MIP 相关的，发现没有。。。于是我做这个可能是迄今为止第一个 Hexo 的 MIP 主题。在经过折腾后发现，Hexo 还是吊吊的，自定义功能很强~

<!-- more -->

## 处理 MIP 规范

由于 MIP 有一些规范，如 `<img>` -> `<mip-img>`，市面上的主题肯定规范校验不通过，那么今天就由一个最简单的主题开始做吧。

### 处理页面 css 样式

思路是在页面生成后 `after_generate` ，获取主题下的 `source/css/**/*.css` ，并获取其内容保存下来，注入辅助函数，手动的 `<head>` 结束前调用方法输出合并后的样式。
### 处理页面 img 标签

思路是在页面渲染后 `after_render:html` ，使用勾子把内容里的 `<img>` 替换为 `<mip-img>` ，代码是：

``` js
hexo.extend.filter.register('after_render:html'，function (html) {
    return html.replace(/<img([\S\s]+?)\/?>/ig，function (match，tag) {
        return '<mip-img ${tag}></mip-img>'.replace('${tag}'，tag.trim());
    });
});
```

<div class="tip-error">
这里只是"暴力"的替换了，并没有处理规范里的宽高，所以在主题里使用图片时，还是需要明确的定义图片的宽高。
</div>

当然也可以做成自动抓取

1. 如果是本地 - 直接获取图片信息，并设置宽高
2. 如果是远程 - 根据链接生成 `md5` 小缀缀，远程下载图片到本地，获取宽高后使用小缀缀设置缓存，最后设置图片宽高

### 处理页面 a 标签

同 `<img>` 标签思路一样，额外加了个判断，判断链接是不是当前页面的链接，如果是则添加 `data-type="mip"` 否则忽略

### 处理页面 canonical 标记

由于必须添加 `canonical` 标记，注入了个辅助方法获取并输出

---

以上解决方法我写成了插件，在开发 Hexo MIP 主题时直接使用就行，代码: <https://github.com/xuexb/hexo-generator-mip>

<div class="tip">
由于只是简单的应用下，打通整体流程，只做了：主页、归档、详情，后续再慢慢扩展吧。
</div>

## 扩展的小提示样式

### 普通引用样式

> 这是一首简单的 `小情歌` ，唱着人们心肠的曲折。我想我很快乐，当有你的温热，脚边的空气转了。
>
> 这是一首简单的 `小情歌` ，唱着我们心头的白鸽。我想我很适合，当一个歌颂者，青春在风中飘着。

### .tip 默认绿色

<div class="tip">
这是一首简单的 `小情歌` ，唱着人们心肠的曲折。我想我很快乐，当有你的温热，脚边的空气转了。
这是一首简单的 `小情歌` ，唱着我们心头的白鸽。我想我很适合，当一个歌颂者，青春在风中飘着。
</div>

### .tip-info 蓝色

<div class="tip-info">
这是一首简单的 `小情歌` ，唱着人们心肠的曲折。我想我很快乐，当有你的温热，脚边的空气转了。
这是一首简单的 `小情歌` ，唱着我们心头的白鸽。我想我很适合，当一个歌颂者，青春在风中飘着。
</div>

### .tip-error 红色

<div class="tip-error">
这是一首简单的 `小情歌` ，唱着人们心肠的曲折。我想我很快乐，当有你的温热，脚边的空气转了。
这是一首简单的 `小情歌` ，唱着我们心头的白鸽。我想我很适合，当一个歌颂者，青春在风中飘着。
</div>


## todo

- 生成的结果进行规范校验
- 添加统计
- 开发其他主流主题

## Link

- [Hexo MIP 主题](https://github.com/xuexb/hexo-theme-mip)
- [Hexo MIP 插件套装](https://github.com/xuexb/hexo-generator-mip) - 助你开发 Hexo 的 MIP 主题
- [Hexo MIP 链接自动推送](https://github.com/xuexb/hexo-mip-push)
