# mixins-sass [![mixins-sass](https://img.shields.io/npm/v/mixins-sass.svg?style=flat-square)](https://www.npmjs.com/package/mixins-sass) [![mixins-sass](https://img.shields.io/npm/dt/mixins-sass.svg)](https://www.npmjs.com/package/mixins-sass)

sass mixins，require `Sass ~> 3.3.0`

**utility**

* [`prefix`](#prefix)
* [`clearfix`](#clearfix)
* [`float`](#float)
* [`text-overflow`](#text-overflow)
* [`animation`](#animation)
* [`placeholder`](#placeholder)
* [`rem`](#rem)
* [`opacity`](#opacity)
* [`arrow`](#arrow)
* [`triangle`](#triangle)
* [`center`](#center)
* [`media`](#media)
* [`box-sizing`](#box-sizing)
* [`touch-scroll`](#touch-scroll)
* [`font`](#font)
* [`onepx`](#onepx)
* [`balloon`](#balloon)
* [`side-line`](#side-line)

**functions**

*string*

* [`str-split`](#str-split)
* [`str-repeat`](#str-repeat)
* [`str-replace`](#str-replace)

*list*

* [`first`](#first)
* [`last`](#last)
* [`prepend`](#prepend)
* [`insert-nth`](#insert-nth)
* [`replace`](#replace)
* [`replace-nth`](#replace-nth)
* [`remove`](#remove)
* [`remove-nth`](#remove-nth)
* [`slice`](#slice)
* [`to-string`](#to-string)
* [`shift`](#shift)
* [`contain`](#contain)

## usage

```shell
npm i mixins-sass --save
```

```scss
@import "./node_modules/mixins-sass/src/mixins";
```

## utility

### `prefix`

```scss
/**
 * @param $map       css列表
 * @param $vendors   浏览器前缀，默认：webkit moz ms o
 */
@mixin prefix($map, $vendors: webkit moz ms o)

.test {
    @include prefix((transliton: all 0.5s ease-out), webkit);
}
```

### clearfix

```scss
@include clearfix;
```

### float

```scss
@include float(left);
```

### text-overflow

文字超出显示省略号，支持多行

```scss
/**
 * @param $line       超出显示省略号的行数，默认：1
 * @param $substract  为预留区域百分比%，默认：0
 */
@mixin text-overflow($line: 1, $substract: 0);
```

### animation

```scss
@include animation(slideUp 900ms ease both) {
    0% {
        transform: translate3d(0, -200px, 0);
    }
    100% {
        transform: translate3d(0, 0, 0);
    }
}
```


### placeholder

```scss
// scss
@include placeholder() {
	...
}
// css
::-webkit-input-placeholder {
    ...
}
::-moz-placeholder {
    ...
}
:-ms-input-placeholder {
   ...
}
```

### rem

px转rem

```scss
/**
 * @param $property       css属性
 * @param $values         css属性值
 * @param $support-ie     是否对不支持rem的浏览器使用px
 * @param $base           基准字体大小，如果不传会搜索全局变量 $base-font，如果没有默认为 16px
 */
@mixin rem($property, $values, $support-ie: true, $base: null)

@include rem('padding', '10px 5px 5px 10px', true, '16px');
```

### opacity

兼容ie的透明度

### arrow

生成上下左右的小箭头：[http://lugolabs.com/caret](http://lugolabs.com/caret)

```scss
/**
 * @param $width
 * @param $border-width
 * @param $direction: top bottom left right
 * @param $background-color
 * @param $position 默认relative
 */
@mixin arrow($width, $border-width, $direction, $color, $background-color, $position: relative)

@include arrow(10px, 1px, 'bottom', '#00f', '#fff');
```

### triangle

三角形生成

```scss
/**
 * @param $width
 * @param $height
 * @param $color
 * @param $direction: top bottom left right
 */
@mixin triangle($width, $height, $color: #000, $direction: bottom)

/**
 * svg背景图生成三角形
 */
@mixin svg-triangle($width, $height, $color: #000, $direction: bottom)

@include triangle(10px, 5px);
```

### center

居中

```scss
/**
 * @param $direction: horizontal vertical both,  default: both
 */
@include center;
```

### media

媒体查询相关

```scss
/**
 * @param $min   min-width
 * @param $max   max-width
 */
@mixin screen($min, $max)
@mixin max-screen($width)
@mixin min-screen($width)
@mixin hidpi($ratio: 1.3)

/**
 * @param $filename
 * @param $retina-filename   多个或者一个
 * @param $ratio             多个或者一个
 * @param $background-size
 */
@mixin retina-image($filename, $retina-filename, $ratio: 1.3, $background-size: 100%)
@mixin iphone6($orientation: all)
@mixin iphone6plus($orientation: all)
@mixin iphone5($orientation: all)
@mixin iphone4($orientation: all)
@mixin ipad($orientation: all)
@mixin ipad-mini($orientation: all)
@mixin ipad-retina($orientation: all)

@include retina-image(test.png, test@2.png test@3.png, 2 3);
```

### box-sizing

```scss
html {
    @include box-sizing(border-box);
}
```

### touch-scroll

```scss
body {
    @include touch-scroll;
}
// css
body {
    -webkit-overflow-scrolling: touch;
    overflow-scrolling: touch;
}
```

### font

中文字体解决方案，来自[https://github.com/zenozeng/fonts.css](https://github.com/zenozeng/fonts.css)，有`font-hei`、`font-kai`、`font-song`、`font-fang-song`。

```scss
body {
    @include font-hei;
}
```

### onepx

移动端`1像素`方案，通过`background-image`渐变色实现

```scss
/**
 * @param $color
 * @param $direction: top bottom left right vertical all,  default: all
 * @param $pseudo: after before, default: after
 */
.border-l {
    @include onepx(#eee, left);
}
```

**onepx-scale**

通过`transform`实现，支持圆角

```scss
/**
 * @param $color
 * @param $direction: top bottom left right vertical all radius,  default: all
 * @param $pseudo: after before, default: after
 * @param $radius default: 1px
 */
.border-r {
    @include onepx-scale(#eee, radius, after, 2px);
}
```

### balloon

气泡提示，来自：[balloon.css](http://kazzkiq.github.io/balloon.css/)

```scss
/**
 * @param $direction:            top bottom left right
 * @param $bg                    气泡提示背景颜色
 * @param $trangle-width         气泡小三角形宽度
 * @param $trangle-height        气泡小三角形高度
 * @param $color                 气泡文字颜色
 * @param $font                  气泡文字大小
 */
@mixin balloon($direction, $bg, $trangle-width: 18px, $trangle-height: 6px, $color: #fff, $font: 12px)

.balloon {
    @include balloon(top, #000);
}
```

```html
<span class="balloon" data-balloon="Whats up!">Hover me!</span>
```

### side-line

线中间夹文字效果

[http://codepen.io/anon/pen/XjNEAR](http://codepen.io/anon/pen/XjNEAR)

```scss
/**
 * @param $height  线高  default: 1px
 * @param $space   线距离文字两边的距离 default: 0.5em
 * @param $color   线颜色 default: inherit
 * @param $style   border-style default: solid
 * @param $adjust  线距离底部的距离，默认垂直居中 default: false
 * @param $double  是否需要两条线
 */
@mixin side-line($height: 1px, $space: 0.5em, $color: inherit, $style: solid, $adjust: false, $double: false)

.side-line {
    @include side-line;
}
```

## functions

**string**

### str-split

字符串分隔

```scss
@function str-split($string, $delimiter: " ")
```

### str-repeat

字符串重复

```scss
@function str-repeat($string, $times)
```

### str-replace

字符串替换

```scss
@function str-replace($string, $search, $replace: "")
```

**list** 

### first

返回列表第一项

```scss
@function first($list)
```

### last

返回列表最后一项

```scss
@function last($list)
```

### prepend

向列表前面插入一个

```scss
@function prepend($list, $value)
```

### insert-nth

向列表某个位置插入

```scss
@function insert-nth($list, $index, $value)
```

### replace

替换列表的某个元素 `$recursive` 是否全部替换

```scss
@function replace($list, $old-value, $new-value, $recursive: false)
```

### replace-nth

替换列表某个位置的元素

```scss
@function replace-nth($list, $index, $value)
```

### remove

删除列表某个元素 `$recursive` 是否删除所有

```scss
@function remove($list, $value, $recursive: false)
```

### remove-nth

删除列表指定位置元素

```scss
@function remove-nth($list, $index)
```

### slice

截取列表中的一部分

```scss
@function slice($list, $start: 1, $end: length($list))
```

### to-string

列表变成字符串，`$glue`为连接符，`$is-nested`是否是嵌套的列表

```scss
@function to-string($list, $glue: '', $is-nested: false)
```

### shift

将列表部分元素前置

```scss
@function shift($list, $index: 1)
```

### contain

列表是存在某个值

```
@function contain($list, $value)
```