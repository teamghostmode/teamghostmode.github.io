---
layout: post
title: "Checking For Collisions Before Spawning"
---

You want to spawn, move, or otherwise place a game object at runtime, but you'd like to make sure it doesn't collide or overlap with any existing objects before you place it.

At first it seems like you could just instantiate the object, wait for an `OnCollisionEnter` to (maybe) fire, and then remove the object if it collided.

But now your spawning logic is split across multiple methods (and multiple frames!), the control flow is confusing and error prone, and you’ve had to add a bunch of additional variables to your class (to communicate between the methods).

Sure it might work, but what was previously some nice and straightforward instantiate / move code, has turned into a bit of a mess.

Fortunately there’s a better approach! The Unity physics engine provides some very handy utility methods for this very purpose. They're called [`CheckSphere`](https://docs.unity3d.com/ScriptReference/Physics.CheckSphere.html), [`CheckBox`](https://docs.unity3d.com/ScriptReference/Physics.CheckBox.html) and [`CheckCapsule`](https://docs.unity3d.com/ScriptReference/Physics.CheckCapsule.html) (and there's also corresponding [`OverlapCircle`](https://docs.unity3d.com/ScriptReference/Physics2D.OverlapCircle.html), [`OverlapBox`](https://docs.unity3d.com/ScriptReference/Physics2D.OverlapBox.html), and [`OverlapCapsule`](https://docs.unity3d.com/ScriptReference/Physics2D.OverlapCapsule.html) methods for 2D games).

Let's take a look a `CheckSphere`. It's the easiest to use, the most efficient, and you'll find it's suitable for the majority of use cases.

In order to use `CheckSphere` you simply provide a position and a radius. The physics system checks against all colliders, returning `true` if any colliders overlap the sphere.

Be sure to tweak the radius to match the game object you’re trying to place, and make sure all of the objects you're checking against have a Collider component attached.

{% highlight csharp %}
Vector3 spawnPosition = new Vector3(10.0f, 1.0f, 14.0f);
float collisionRadius = 4.0f;

bool didHit = Physics.CheckSphere(spawnPosition, collisionRadius);
if (didHit) {
    // Can't place at this position, try somewhere else.
} else {
    // Nothing was hit, it's ok to place our object here.
}
{% endhighlight %}

So much better! The code is simple, short, self-contained, and easy to follow (and therefore much easier to debug!). 

If you want to only check for collisions against certain objects (eg. check against buildings, but not foliage or ground), you can also provide a layer mask like so:

{% highlight csharp %}
int buildingsLayer = LayerMask.NameToLayer("Buildings");
Physics.CheckSphere(spawnPosition, collisionRadius, buildingsLayer);
{% endhighlight %}

Just make sure you have a “Buildings” layer that all of your buildings are assigned to.
