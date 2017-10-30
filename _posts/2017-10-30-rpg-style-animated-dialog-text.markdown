---
layout: post
title: "RPG Style Animated Dialog Text"
---
*Question: In Unity, how do I get the text in my dialog boxes to type out character by character, to give the speaking effect seen in many RPG games?*

Using an animated 'talking' effect like this is very common, and dialog screens can look a little off without it. It’s a small detail, but it can make all the difference.

<figure>
  <iframe src='https://gfycat.com/ifr/FaintFirsthandDiscus' frameborder='0' scrolling='no' width='319' height='95'></iframe>
  <figcaption>Animated dialog text</figcaption>
</figure>

So how do you go about doing this in Unity? Getting text to display all at once is simple enough, but when it comes to animating the text, it's hard to know where to even start. That is, until you get familiar with Unity's coroutines.

Any time you want an action to occur over multiple frames (instead of all at once), coroutines are often a good approach. Coroutines let you use the `yield` keyword, which pauses the execution of a function for a specified time (while the rest of the game keeps running).

You can animate text with a coroutine as follows:

{% highlight csharp %}
private IEnumerator AnimateTextCoroutine(string text) {
    TextField.text = "";
    var wait = new WaitForSeconds(0.01f);

    for (int charIndex = 0; charIndex < text.Length; ++charIndex) {
        TextField.text += text[charIndex];
        yield return wait;
    }
}
{% endhighlight %}

This loops over a string, character by character, appending each character to a TextField and waiting for 0.01 seconds before continuing to the next character.

You can use this coroutine in an `AnimatedDialog` class as follows:
{% highlight csharp %}
using System.Collections;

using UnityEngine;
using UnityEngine.UI;

public class AnimatedDialog : MonoBehaviour {
    public float DelayBetweenChars = 0.01f;
    public Text TextField;

    public void AnimateText(string text) {
        StartCoroutine(AnimateTextCoroutine(text));
    }

    private IEnumerator AnimateTextCoroutine(string text) {
        TextField.text = "";
        var wait = new WaitForSeconds(DelayBetweenChars);

        for (int charIndex = 0; charIndex < text.Length; ++charIndex) {
            TextField.text += text[charIndex];
            yield return wait;
        }
    }
}
{% endhighlight %}

<span class="muted">(Note that we [don’t use strings to start the coroutine]({% post_url 2017-10-19-dont-start-coroutines-with-strings %}))</span>

Attach both an `AnimatedDialog` component and a UI `Text` component to a game object, and be sure to set the `TextField` reference in the inspector.

Now, call the public `AnimateText` function with the text you want to animate. For example, an `NPC` class could use the `AnimatedDialog` class as follows:
{% highlight csharp %}
using UnityEngine;

public class NPC : MonoBehaviour {
    public AnimatedDialog DialogBox;
    public string DialogText;

    public void OnPlayerInteract() {
        DialogBox.AnimateText(DialogText);
    }
}
{% endhighlight %}

Again, be sure to set the `DialogBox` and `DialogText` in the inspector.
