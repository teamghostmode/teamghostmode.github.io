---
layout: post
title:  "Custom Icons For Scriptable Objects"
---
If you ever want to distract yourself from actually working on your game, I highly recommend customizing your editor setup, it's a personal favourite time waster of mine.

<figure>
  <img src="{{site.url}}/assets/images/scriptable-object-cusom-icon.png" alt="Custom Icons For Scriptable Objects"/>
  <figcaption>Scriptable objects with custom icons</figcaption>
</figure>

Using custom icons for scriptable objects adds a bit of life to your project window, and helps you to understand your asset types at a glance. To do it:

1. Add some icons to your assets folder
2. Select a `ScriptableObject` C# script in the project window
3. In the inspector, click the icon in the top left (it has a dropdown arrow)
4. Click the ‘Other…’ button
5. Finally, select your icon from the list of texture assets

If the dropdown won't show, make sure you've selected the C# script that contains your `ScriptableObject` class, and not an asset created *from* the scriptable object.

<figure>
  <img src="{{site.url}}/assets/images/scriptable-object-cusom-icon-dropdown.png" alt="Custom Icon Dropdown"/>
  <figcaption>The custom icon dropdown menu</figcaption>
</figure>

Now any assets of this type will be assigned the icon you selected.

If you like the icons used in the example above, [you can grab them from here](https://7soul1.deviantart.com/art/16x16-RPG-Icons-Pack-1-Free-Sample-467188465).
