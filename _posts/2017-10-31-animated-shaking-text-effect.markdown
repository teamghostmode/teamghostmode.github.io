---
layout: post
title: "Animated Shaking Text Effect"
---

Games like Undertale occasionally use a shaking text effect when displaying dialog, which helps to give moments a lot more impact.

<figure>
  <iframe src='https://gfycat.com/ifr/JovialComplexBighornsheep' frameborder='0' scrolling='no' width='500' height='191'></iframe>
  <figcaption>Shaking text effect in Undertale</figcaption>
</figure>
 
So how do you implement this shaking text effect in Unity? It’s not too hard to animate a block of text all together, but how do you get each character to move individually?

First, just as with the [wavy text effect]({% post_url 2017-11-01-animated-wavy-text-effect %}), you have to break up your text so each character is a seperate game object. That way they each have a seperate transform and can be moved around independently.

Then attach the following `ShakeEffect` script to each game object:

{% highlight csharp %}
using UnityEngine;

public class ShakeEffect : MonoBehaviour {
    public float Magnitude = 0.5f;

    private Vector3 m_startPos;

    private void Start() {
        m_startPos = transform.localPosition;
    }

    private void Update() {
        float x = Random.Range(-Magnitude, Magnitude);
        float y = Random.Range(-Magnitude, Magnitude);
        transform.localPosition = m_startPos + new Vector3(x, y, 0.0f);
    }
}
{% endhighlight %}

Be sure to tweak the `Magnitude` to your liking in the inspector.

<figure>
  <iframe src='https://gfycat.com/ifr/InbornOpenBunny' frameborder='0' scrolling='no' width='610' height='238' allowfullscreen></iframe>
  <figcaption>Shaking text effect in Unity</figcaption>
</figure>

The `ShakeEffect` script works by updating the local position every frame, offsetting it from it’s start position by a random x and y value based on the `Magnitude` field.
