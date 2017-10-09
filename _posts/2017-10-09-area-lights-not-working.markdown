---
layout: post
title:  "Why Your Area Lights Aren’t Working"
---
You’ve got directional lights and point lights that are lighting up your scene just fine, but area lights don’t seem to be working at all! What’s the deal?

Unity’s area lights work a little differently. Their lighting calculation is very processor intensive, and therefore needs to be precalculated and ‘baked’ into a lightmap.

You can do this by opening the lighting settings window (Window → Lighting → Settings), and clicking ‘Generate Lighting’ at the very bottom. If the button is greyed out, you’ll need to uncheck ‘Auto Generate’ first.

<figure>
  <img src="{{site.url}}/assets/images/generate_lighting.png" alt="Generate Lighting"/>
  <figcaption>Click 'Generate Lighting' to bake a lightmap</figcaption>
</figure>

Unity will start baking a lightmap, and it may take a while! But once it’s done, your area lights should working like you'd expect.
