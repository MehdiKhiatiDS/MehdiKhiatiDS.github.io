---
layout: post
title: Do we have Linear Regression!
subtitle: Yes we do, or do we!
gh-repo: mehdikhiati.com
gh-badge: [star, fork, follow]
tags: [test]
comments: true
---

You can write regular [markdown](http://markdowntutorial.com/) here and Jekyll will automatically convert it to a nice webpage.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](http://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

**Tweaking Stuff**

## Ok now we about to AI this *itch!!

Here's a useless table: Just kidding its not my phone number for nerdy updates and hinge and all!

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |


Here's a code chunk, that will show you a quick tree install I did for diamonds classification!
Pretty neat ay!

~~~
!pip install graphviz
!apt-get install graphviz

import graphviz
from sklearn.tree import export_graphviz

dot_data = export_graphviz(model, out_file=None, feature_names=features, filled=True, rotate=True)
graphviz.Source(dot_data)
~~~

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box hinge might be fuego.

### Warning

{: .box-warning}
**Warning:** This is a warning box run.

### Error

{: .box-error}
**Error:** This is an error box ughh lol.
