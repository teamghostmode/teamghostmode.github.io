---
layout: post
title:  "Using UI Toggle’s OnValueChanged"
---
You’ve hooked up your toggle’s OnValueChanged in the inspector, your function is called, but the value passed in is either always true or always false.

This one’s a Unity gotcha that’s unintuitive but easily fixed.

Let’s use a toggle that controls mute on/off as an example. In our audio manager we have the function to be called when the toggle value changes. Nothing special here.

{% highlight csharp %}
public void OnMuteToggled(bool isChecked) {
    if (isChecked) {
        // Mute the game.
        AudioListener.volume = 0.0f;
    } else {
        // Un-mute the game.
        AudioListener.volume = 1.0f;
    }
}
{% endhighlight %}

Now here’s the trick. When selecting the `OnMuteToggled` function in the toggle’s inspector, make sure you select the one under ‘Dynamic bool’.

<figure>
  <img src="{{site.url}}/assets/images/dynamic-bool.png" alt="Dynamic Bool"/>
  <figcaption>Select the function listed under 'Dynamic bool'</figcaption>
</figure>

That's all. Now when the control is toggled, the function will receive the correct bool parameter according to the toggle’s current state.
