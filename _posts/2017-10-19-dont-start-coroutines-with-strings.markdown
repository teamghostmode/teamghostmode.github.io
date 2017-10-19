---
layout: post
title:  "Don't Start Coroutines With Strings"
---

I see a lot of Unity projects using coroutines like this:

{% highlight csharp %}
StartCoroutine("SpawnEnemies");
{% endhighlight %}

This starts a coroutine by passing the name of the method as a string. And it works fine, so what’s the problem?

The problem is that using strings like this provides no error checking! The compiler is very powerful and can find all kinds of bugs for you, but not if you use strings like this!

Maybe you typo the method’s name (easy to do since strings don’t auto-complete), or you refactor and change the method’s name, or you just delete the method entirely. The compiler can automatically detect all of these bugs for you, provided you’re *not using strings.* Please don’t waste your time by having to find these errors manually.

So how do we get that string out of here, and let the compiler help us? Just start your coroutine by **calling** the method. The difference is subtle, but important:

{% highlight csharp %}
StartCoroutine(SpawnEnemies());
{% endhighlight %}

That's it! You've successfully befriended the compiler, a truely loyal companion that shall remain by your side, dutifully bringing bugs to your attention.
