---
layout: post
title: "Checking For Collisions Before Spawning"
---

You want to spawn, move, or otherwise place a game object at runtime, but you'd like to make sure it doesn't collide or overlap with any existing objects before you place it.

At first it seems like you could just instantiate the object, wait for an `OnCollisionEnter` to (maybe) fire, and then remove the object if it collided.

But now your spawning logic is split across multiple methods (and multiple frames!), the control flow is confusing and error prone, and you’ve added a bunch of additional variables to your class (since these methods can’t communicate directly).

Sure it might work, but what was previously some nice and straightforward instantiate / move code, has turned into a bit of a mess.

Fortunately there’s a better approach! The Unity physics engine provides a very handy utility function called [`OverlapSphere`](https://docs.unity3d.com/ScriptReference/Physics.OverlapSphere.html) (and [`OverlapCircleAll`](https://docs.unity3d.com/ScriptReference/Physics2D.OverlapCircleAll.html) for 2D).

In order to use `OverlapSphere` you simply provide a position and a radius, and the physics engine will return an array of colliders that are within that sphere. If an empty array is returned, you know that you can place your game object at that position.

Just be sure to tweak the radius to match the game object you’re trying to place, and make sure all your objects have a Collider component of some sort attached.

{% highlight csharp %}
Vector3 spawnPos = new Vector3(10.0f, 1.0f, 14.0f);
float collisionRadius = 4.0f;

Collider[] hitColliders = Physics.OverlapSphere(spawnPos, collisionRadius);
if (hitColliders.Length == 0) {
    // No collisions, ok to spawn game object.
    Instantiate(prefab, spawnPos, Quaternion.identity);
} else {
    // Found a collision, try a different spawn position.
}
{% endhighlight %}

So much better! The code is simple, short, self-contained, and easy to follow (and therefore much easier to debug!). 

If you want to only check for collisions against certain objects (eg. check against buildings, but not foliage or ground), you can also provide a layer mask like so:

{% highlight csharp %}
int buildingsLayer = LayerMask.NameToLayer("Buildings");
Physics.OverlapSphere(spawnPos, collisionRadius, buildingsLayer);
{% endhighlight %}

Just make sure you have a “Buildings” layer that all of your buildings are assigned to.

Also, if a sphere doesn’t quite suit your needs, Unity provides [`OverlapBox`](https://docs.unity3d.com/ScriptReference/Physics.OverlapBox.html) and [`OverlapCapsule`](https://docs.unity3d.com/ScriptReference/Physics.OverlapCapsule.html) methods. And lastly, if this an action you’re performing frequently, you’ll want to check out [`OverlapSphereNonAlloc`](https://docs.unity3d.com/ScriptReference/Physics.OverlapSphereNonAlloc.html) to prevent garbage generation.
