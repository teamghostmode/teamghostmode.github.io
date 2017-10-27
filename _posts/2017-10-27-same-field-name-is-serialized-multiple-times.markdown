---
layout: post
title: "Unity Error: The same field name is serialized multiple times in the class or its parent class"
---
Out of nowhere this obscure error has started showing up in your console:

<div class="highlighter-rouge"><pre class="highlight"><code style="white-space:pre-wrap;">The same field name is serialized multiple times in the class or its parent class. This is not supported.
UnityEngine.GUIUtility:ProcessEvent(Int32, IntPtr)
</code></pre></div>

So, what does it mean, what’s causing the error, and how do you fix it?

Firstly, sometimes this error just shows up due to a bug in Unity / MonoDevelop. You can fix it by simply closing Unity and MonoDevelop, then re-opening them.

If that doesn’t do the trick, then you’ve likely got a legitimate error in your code. The error occurs when a sub-class declares a variable with the same name as an existing variable in its base-class. For example:

{% highlight csharp %}
// Base-class
public class Enemy : MonoBehaviour {
    public int Health;
}

// Sub-class
public class RangedEnemy : Enemy {
    public int Health;
}
{% endhighlight %}

Here `RangedEnemy` inherits the `Health` field from `Enemy`, but also declares it’s own `Health` field. This causes a clash when Unity tries to serialize your game object.

In order to fix this, you need to rename or remove the duplicate variable. In the example above, you would solve this by removing the `Health` field from `RangedEnemy`. Since `RangedEnemy` already inherits the `Health` field from `Enemy`, there’s no need to define it again.
