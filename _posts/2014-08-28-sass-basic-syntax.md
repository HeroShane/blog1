---
layout: post
title: Sass基本语法学习
categories:
    - 前端
tags:
    - sass
excerpt: 根据官网整理的Sass文档    
---

## Referencing Parent Selector: &
{% highlight css %}
#main {
  color: black;
  &-sidebar { border: 1px solid; }
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
#main {
  color: black;
  &-sidebar { border: 1px solid; }
}
{% endhighlight %}

## Nested Properties
{% highlight css %}
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
.funky {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold; }
{% endhighlight %}

## Viriable:$

{% highlight css %}
$width: 5em;
#main {
  width: $width;
}

{% endhighlight %}

{% highlight css %}
#main {
  $width: 5em !global;
  width: $width;
}

#sidebar {
  width: $width;
}
{% endhighlight %}

## @mixin

{% highlight css %}
@mixin firefox-message($selector) {
  body.firefox #{$selector}:before {
    content: "Hi, Firefox users!";
  }
}

@include firefox-message(".header");
{% endhighlight %}

*is compiled to:*

{% highlight css %}
body.firefox .header:before {
  content: "Hi, Firefox users!"; }
{% endhighlight %}

## Interpolation

{% highlight css %}
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
p.foo {
  border-color: blue; }
{% endhighlight %}

## extends

{% highlight css %}
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
.error, .seriousError {
  border: 1px #f00;
  background-color: #fdd;
}

.seriousError {
  border-width: 3px;
}
{% endhighlight %}

## @for

{% highlight css %}
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
.item-1 {
  width: 2em; }
.item-2 {
  width: 4em; }
.item-3 {
  width: 6em; }
{% endhighlight %}

## @each

{% highlight css %}
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
.puma-icon {
  background-image: url('/images/puma.png'); }
.sea-slug-icon {
  background-image: url('/images/sea-slug.png'); }
.egret-icon {
  background-image: url('/images/egret.png'); }
.salamander-icon {
  background-image: url('/images/salamander.png'); }
{% endhighlight %}
-----------------------------------------------------------
{% highlight css %}
@each $header, $size in (h1: 2em, h2: 1.5em, h3: 1.2em) {
  #{$header} {
    font-size: $size;
  }
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
h1 {
  font-size: 2em; }
h2 {
  font-size: 1.5em; }
h3 {
  font-size: 1.2em; }
{% endhighlight %}

## @while

{% highlight css %}
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
.item-6 {
  width: 12em; }

.item-4 {
  width: 8em; }

.item-2 {
  width: 4em; }
{% endhighlight %}

## @if

{% highlight css %}
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
{% endhighlight %}

*is compiled to:*

{% highlight css %}
p {
  color: green; }
{% endhighlight %}

## Minxin

{% highlight css %}
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
{% endhighlight %}

*is compiled to:*

{% highlight css %}
.page-title {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
  padding: 4px;
  margin-top: 10px; }
{% endhighlight %}

-----------------------------------
{% highlight css %}
@mixin silly-links {
  a {
    color: blue;
    background-color: red;
  }
}

@include silly-links;
{% endhighlight %}

*is compiled to:*

{% highlight css %}
a {
  color: blue;
  background-color: red; }
{% endhighlight %}































































