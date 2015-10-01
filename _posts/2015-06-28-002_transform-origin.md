---
layout: post
title:  "transform-origin"
categories: frontend
tags: [html, css]
---

<style>
.example1 {
    background-color: gainsboro;
    height: 300px;
    position: relative;
}
.example1-item {
    background-color: pink;
    left: 50%;
    line-height: 40px;
    margin: -20px 0 0 -100px;
    position: absolute;
    text-align: center;
    top: 50%;
    transform: scale(1.78);
    width: 200px;
}
.example2 {
    background-color: gainsboro;
    overflow: hidden;
}
.example2-item {
    background-color: pink;
    float: right;
    line-height: 40px;
    margin: 100px 0;
    text-align: center;
    transform: scale(1.78);
    width: 200px;
}
.origin-fixed {
    transform-origin: right top;
}
</style>

Recently I used `transform` property in one of my projects. `Scale()`, to be precise. It works in a funny way: changes the scale of an element but not its initial size or position. Upside is that coder doesn’t have to calculate any absolute value because browser does that. It would be easy to double width with `scale(2)` but with `scale(1.78)` it would start to get tricky. Thanks to scaling nature we don’t have to bother with such nuances.

<div class="example1">
    <span class="example1-item">Element scaled 1.78 times.</span>
</div>

{% highlight css %}
.example1 {
    background-color: gainsboro;
    height: 300px;
    position: relative;
}
.example1-item {
    background-color: pink;
    left: 50%;
    line-height: 40px;
    margin: -20px 0 0 -100px; /* halves of height, and width */
    position: absolute;
    text-align: center;
    top: 50%;
    transform: scale(1.78);
    width: 200px;
}
{% endhighlight %}

The above example shows a scenario in which a coder doesn’t have to worry about element’s surrounding. In a perfect world we would always have situations like that. But in this, not being a perfect world, we can encounter something like this:

<div class="example2">
    <span class="example2-item">Element scaled 1.78 times.</span>
</div>

{% highlight css %}
.example2 {
    background-color: gainsboro;
    overflow: hidden;
}
.example2-item {
    background-color: pink;
    float: right;
    line-height: 40px;
    margin: 100px 0;
    text-align: center;
    transform: scale(1.78); /* play with it in web inspector */
    width: 200px;
}
{% endhighlight %}

[_sic_]

Description: element is floated right and scaled. As a result some part of scaled element goes outside of its container. It can be cut off by `overflow: hidden` or even worse, leak under surrounding element (like sidebar). In other words, not something we would show to friends or our client. That’s where `transform-origin` comes into play. It’s a property that helps us to establish the origin for transformation. By default, its value is `50% 50% 0`, which in 2D context translates into a center of an element. In most cases it’s a desired effect. But not always, as I experienced last week.

So, in problematic situation I used:

{% highlight css %}
.origin-fixed {
    transform-origin: right top;
}
{% endhighlight %}

The values can be absolute, relative, or keywords, as above. The effect:

<div class="example2">
    <span class="example2-item origin-fixed">Element scaled 1.78 times.</span>
</div>

Another triumph of mind over matter.

## Further reading

* [Article about `transform-origin` on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin)