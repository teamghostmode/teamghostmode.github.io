---
layout: post
title: "Unity Tip: Random Perlin Noise"
---

How do you use Unity’s Mathf.PerlinNoise to generate random noise?

Unity’s perlin noise method will always return the exact same value for any given x and y coordinate. Let’s look at how to inject some randomness into the noise we generate, by offsetting the location that we sample from.

First we need a random x and y offset:

{% highlight csharp %}
float maxOffset = 1000.0f;
float xOffset = Random.Range(0.0f, maxOffset);
float yOffset = Random.Range(0.0f, maxOffset);
{% endhighlight %}

(Tweak the max offset until you find one that gives good results for your project)

Then we simply offset our x and y values before sampling:

{% highlight csharp %}
float xCoord = (x + xOffset) / Width * Scale;
float yCoord = (y + yOffset) / Height * Scale;
float sample = Mathf.PerlinNoise(xCoord, yCoord);
{% endhighlight %}

That’s it! We’ve now randomised our perlin noise generation.

Let’s use this approach to generate a random perlin noise texture:

{% highlight csharp %}
using UnityEngine;

public class RandomPerlinNoise : MonoBehaviour {

    public int Width  = 256;
    public int Height = 256;
    public float Scale = 10.0f;
    public float MaxOffset = 1000.0f;

    private Color[] m_pixels;
    private Texture2D m_texture;

    private void Start() {
        m_texture = new Texture2D(Width, Height);
        m_pixels = new Color[Width * Height];

        var meshRenderer = GetComponent<Renderer>();
        meshRenderer.material.mainTexture = m_texture;
    }

    private void Update() {
        RandomizeTexture();
    }

    private void RandomizeTexture() {
        float xOffset = Random.Range(0.0f, MaxOffset);
        float yOffset = Random.Range(0.0f, MaxOffset);

        float y = 0.0f;
        while (y < Height) {
            float x = 0.0f;
            while (x < Width) {
                float xCoord = (x + xOffset) / Width * Scale;
                float yCoord = (y + yOffset) / Height * Scale;
                float sample = Mathf.PerlinNoise(xCoord, yCoord);

                Color pixel = new Color(sample, sample, sample);
                m_pixels[(int)y * Width + (int)x] = pixel;

                x++;
            }

            y++;
        }

        m_texture.SetPixels(m_pixels);
        m_texture.Apply();
    }
}
{% endhighlight %}

Just attach this script to a plane, and run the project. A random perlin noise texture will be generated every frame.
