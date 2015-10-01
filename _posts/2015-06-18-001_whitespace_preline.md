---
layout: post
title:  "white-space: pre-line"
categories: frontend
tags: [html, css]
---

One of less known things in CSS is `white-space` property `pre-line` value.

{% highlight css %}
.nl2br {
    white-space: pre-line;
}
{% endhighlight %}

Let’s take this paragraph,

{% highlight html %}
<p>This is a text which has endlines
quite often which in return makes
it easier to read ‘cause lines
don’t go to any great lengths.</p>
{% endhighlight %}

Normally it would render all in one line:

_This is a text which has endlines
quite often which in return makes
it easier to read ‘cause lines
don’t go to any great lengths._

It happens like that because browser ignores most of white space: all spaces, tabs, and new lines become a single space character. But when we use `white-space: pre-line`, it looks like that:

<p style="white-space: pre-line;"><em>This is a text which has endlines
quite often which in return makes
it easier to read ‘cause lines
don’t go to any great lengths.</em></p>

It behaves much like PHP’s function `nl2br()`. It remains relatively unknown; in my career I had used that only on two occasions.

## Further reading

* [Article about `white-space` on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space)