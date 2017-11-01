---
layout: post
title: "Animated Wavy Text Effect"
---
The dialog system in Shovel Knight sometimes uses a really nice ‘wavy’ text animation, like when talking to the bard for example:

<figure>
  <iframe src='https://gfycat.com/ifr/ImmenseMajorAcouchi' frameborder='0' scrolling='no' width='600' height='81'></iframe>
  <figcaption>Wavy text effect in Shovel Knight</figcaption>
</figure>

So how do you go about recreating this in Unity? Is it possible to animate the individual characters in a text component? And how do you get a nice and smooth wavy motion to the animation?

Much like the [shaking text effect]({% post_url 2017-10-31-animated-shaking-text-effect %}), you first need to take your text and seperate out each character into it’s own game object. This allows you to animate them individually.

Then attach the following `WaveEffect` script to each character:

{% highlight csharp %}
using UnityEngine;

public class WaveEffect : MonoBehaviour {
    public float Frequency = 8.0f;
    public float Magnitude = 1.5f;
    public float Offset;

    private Vector3 m_startPos;

    private void Start() {
        m_startPos = transform.localPosition;
    }
    
    private void Update() {
        float y = Mathf.Sin((Offset + Time.time) * Frequency) * Magnitude;
        transform.localPosition = m_startPos + new Vector3(0.0f, y, 0.0f);
    }
}
{% endhighlight %}

Then set the `Offset` value in the inspector for each game object. Each character should have a slightly larger offset than the one before it (I used 0.00, 0.10, 0.15, etc).

You can tweak the `Frequency` and `Magnitude` fields in the inspector to your liking. Just make sure all characters use the same frequency and magnitude settings, to keep the wavy effect in sync.

<figure>
  <iframe src='https://gfycat.com/ifr/UnkemptGlisteningHapuku' frameborder='0' scrolling='no' width='600' height='222'></iframe>
  <figcaption>Wavy text effect in Unity</figcaption>
</figure>

The `WaveEffect` script works by updating the local position’s y value every frame, using a sine wave based on the current game time, to produce a smooth, wavy motion.
