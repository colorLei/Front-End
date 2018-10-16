## 语法
-  SCSS (Sassy CSS) CSS3 语法的扩充版本 .scss
-  Sass 缩排语法 .sass


```
# 将 Sass 转换为 SCSS
$ sass-convert style.sass style.scss

# 将 SCSS 转换为 Sass
$ sass-convert style.scss style.sass
```
## CSS Extensions
###### Nested Rules
###### 引用父选择符： &
###### 嵌套属性

```
.funky {
  font: 2px/3px {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```
###### Variables: $

```
$width: 5em;

#main {
  width: $width;
}

```
###### Interpolation: #{}

```
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
```
## 运算
## `@`规则和指令

######  ==@import==
> Sass 扩展了 CSS 的 @import 规则，让它能够引入 SCSS 和 Sass 文件。 所有引入的 SCSS 和 Sass 文件都会被合并并输出一个单一的 CSS 文件。 另外，被导入的文件中所定义的变量或 mixins 都可以在主文件中使用。

######  ==@media==

```
.sidebar {
  width: 300px;
  @media screen and (orientation: landscape) {
    width: 500px;
  }
}
```
######  ==@extend==

```
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```
######  ==@extend-Only Selectors==

```
// This ruleset won't be rendered on its own.
#context a%extreme {
  color: blue;
  font-weight: bold;
  font-size: 2em;
}
```
> However, placeholder selectors can be extended, just like classes and ids. The extended selectors will be generated, but the base placeholder selector will not. 例如：

```
.notice {
  @extend %extreme;
}
```
######  ==@debug==
######  ==@warn==
######  ==@if==

```
p {
  @if 1 + 1 == 2 { border: 1px solid;  }
  @if 5 < 3      { border: 2px dotted; }
  @if null       { border: 3px double; }
}

$type: monster;
p {
  @if $type == ocean {
    color: blue;
  } @else if $type == matador {
    color: red;
  } @else if $type == monster {
    color: green;
  } @else {
    color: black;
  }
}
```
######  ==@for==

```
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
```
######  ==@each==

```
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}
```
######  ==@while==

```
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}

```
######  ==@mixin==
######  Including a Mixin: ==@include==

```
@mixin compound {
  @include highlighted-background;
  @include header-text;
}

@mixin highlighted-background { background-color: #fc0; }
@mixin header-text { font-size: 20px; }
```
- Arguments

```
@mixin sexy-border($color, $width: 1in) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue); }
h1 { @include sexy-border(blue, 2in); }
```

- `...`

```
@mixin box-shadow($shadows...) {
  -moz-box-shadow: $shadows;
  -webkit-box-shadow: $shadows;
  box-shadow: $shadows;
}

.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}

----------------------------------------------------------

$values: #ff0000, #00ff00, #0000ff;
.primary {
  @include colors($values...);
}

```
## Function Directives

```
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
  @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); }
```

