---
layout: post
title:  "Unity Tip: Auto-Pause On Error"
---
We’ve all had it happen, your game spits an error into the console at runtime and you don’t even realize. Especially when the error doesn’t cause something game breaking or visually obvious.

Hopefully you’ll notice it at some point and think “When the hell did that happen?”, but it’s also possible that you’ll just miss it entirely.

Unity has an easily overlooked feature called ‘Error Pause’, you’ll find the button along the top of the console. Turning on ‘Error Pause’ will automatically pause execution of your game the instant an error is logged (including unhandled exceptions and failed assertions).

<figure>
  <img src="{{site.url}}/assets/images/auto-pause-on-error.png" alt="Auto-Pause On Error"/>
  <figcaption>Turn on 'Error Pause' above the console</figcaption>
</figure>

No longer will an error go unnoticed in the console! And better still, it’s immensely helpful to know the exact moment an error occurred, /and/ be able to inspect the game’s state at the time of error.
