---
layout: post
title:  "Using billboards with SEGI"
---
So you’ve grabbed the [newly open sourced SEGI](https://forum.unity.com/threads/segi-fully-dynamic-global-illumination.410310/) (Sonic Ether Global Illumination) asset. You love that you don’t have to bake for 30 hours every time you make a change in your scene, but now your billboard particles and line renderers don’t face the camera!

Fortunately there’s an easy fix, using layers and SEGI’s GI Culling Mask.

1. Create a new layer, “BillboardFX” for example.
2. Assign all your billboard game objects to the “BillboardFX” layer.
3. In SEGI's main configuration, find the ‘GI Culling Mask’ setting.
4. Uncheck “BillboardFX” in the GI Culling Mask dropdown.

<figure>
  <img src="{{site.url}}/assets/images/SEGI_billboards.png" alt="SEGI Billboards"/>
  <figcaption>The GI Culling Mask dropdown in SEGI's main configuration</figcaption>
</figure>
