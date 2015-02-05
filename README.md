# CreditCloud 代码风格指导

本文主要参考了 [@mdo 的代码风格](http://codeguide.bootcss.com/)，这里从中摘选了需要被强调的部分，以及给出了在 CreditCloud 实践中与其不一样的地方。以下所列的风格指导在 CreditCloud P2P 产品开发中必须遵守，而 @mdo 的风格作为推荐可做参考。

本文包括对 HTML 和 CSS 的代码风格指导。

## 通用

* 不使用 tab 制表符，无论是 HTML、CSS 还是 JS 文件均使用 4 个空格作为缩进，请设置编辑器将 tab 键自动输出 4 个空格
* 设置编辑器将文件保存为 UTF-8 编码

## 文件组织

静态文件均放在 `/assets` 目录下，CSS/Less 文件放在 `/assets/css` 下，JS 文件放在 `/assets/js` 下，图片文件放在 `/assets/img` 下。

对于代码中的文件引用地址，均使用 `/assets` 开头的绝对路径，而不使用相对路径。所以需要运行 P2P 开发代码或者启动静态文件服务器，访问相应的本机服务器的 `http://` 开头的地址，而不是直接访问静态文件（浏览器地址以 `file://` 开头）

## HTML

### 语法

* 对于属性的定义，确保全部使用双引号，绝不要使用单引号。
* **必须**在自闭合（self-closing）元素（如 `link`、`img` 的尾部添加斜线 `<img scr="/assets/a.jpg" alt="..." />` -- 虽然在 HTML5 规范中是可选的，但是这个结尾斜线对我们使用的模板解析器来说是必须的。
* 不要省略可选的结束标签（closing tag）（例如，`</p>`、`</li>` 或 `</body>`）。

### HTML5 doctype
必须添加 doctype，一般是加到 layout 文件头部：`<!DOCTYPE html>`

### head

添加以下这些标签在 `<head>` 中

* 指定字符编码：`<meta charset="UTF-8">`
* 指定国产套壳浏览器使用 webkit 内核：`<meta name="renderer" content="webkit">`
* 不让百度搜索结果为用户返回你的网站“移动版”：`<meta http-equiv="Cache-Control" content="no-siteapp" />`

### 引入外部文件

前面文件组织这部分提到过，引用 CSS、JS 及图片文件均使用 `/assets/` 开头的绝对路径。不使用 `@import` 引入 CSS 而只使用 `<link>` 标签，不使用不必要的 type 属性。

## CSS

### reset & base

使用 `<link rel="stylesheet" href="/assets/css/base.css">` 这个文件包含了 [typo.css](http://typo.sofi.sh/) 作为 CSS Reset，包含了除了 normalize.css(reset 功能) 的 Bootstrap 框架，[font-awesome](http://fortawesome.github.io/Font-Awesome/) 以及 [pure.css 的网格系统](http://purecss.io/grids/)。请在此基础上开发。

可以通过改变 variables.less 文件改变 base.css 的默认值，注意 base.css 只在静态文件服务器启动后第一次访问时编译，如改动过 base.less 或 variables.less，需重启静态文件服务器。

### grids

不使用 Bootstrap 的网格系统，使用 Pure.css 的，注意 `.pure-g` `.pure-u-*` class 名改为 `.p-g` `.p-u-*`，并且添加了 7 等分的网格（用于日历）。

```html
<div class="p-g">
    <div class="p-u-1-5">1/5</div>
    <div class="p-u-4-5">
        <div class="p-g">
            <div class="p-u-1-7">1/7</div>
            <div class="p-u-1-7">1/7</div>
            <div class="p-u-1-7">1/7</div>
            <div class="p-u-1-7">1/7</div>
            <div class="p-u-1-7">1/7</div>
            <div class="p-u-1-7">1/7</div>
            <div class="p-u-1-7">1/7</div>
        </div>
    </div>
</div>
