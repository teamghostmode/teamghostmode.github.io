---
layout: post
title:  "Unity Tip: Multi-line String Inspector"
---
By default strings are only given a single-line textfield in the inspector. When working with longer strings this quickly becomes a pain, as reading and editing strings in such a small area can be annoying and error prone.

You know you could solve this with a custom editor or property drawer, but for something so simple that just seems like overkill.

Ideally the string would be displayed as a multi-line textarea. Thankfully Unity provides an easy way to do just that, using the `[TextArea]` attribute.

Say you have a string for an NPC dialog, just use the attribute as follows:

{% highlight csharp %}
[TextArea(4, 6)] // ‘4’ sets the minimum size, and ‘6’ sets the maximum.
public string Dialog;
{% endhighlight %}

<figure>
  <img src="{{site.url}}/assets/images/multi_line_string_inspector.png" alt="String Inspector"/>
  <figcaption>Multi-line textarea in the inspector</figcaption>
</figure>

Your string will now display as a textarea in the inspector.

This handy feature also works for string arrays!

{% highlight csharp %}
[TextArea(4, 6)]
public string[] Dialogs;
{% endhighlight %}

<figure>
  <img src="{{site.url}}/assets/images/multi_line_string_array_inspector.png" alt="String Array Inspector"/>
  <figcaption>An array of multi-line textareas in the inspector</figcaption>
</figure>
