---
layout: blogpost
title: "My First Firefox Plugin"
---

 Funimation is a decent place to find a lot of good dubbed anime. The website however has a few things about it that annoy me, but by far the worst thing about it is its habit of showing episode spoilers in thumbnails and video pre-load images. Recently it annoyed me so much I made a Firefox plugin to hide spoilers on the site.

So here it is: [Funimation Spoiler Blocker on Mozilla.org](https://addons.mozilla.org/en-US/firefox/addon/funimation-spoiler-blocker/)

<img src="/assets/img/blog/firefox-plugin/plugin.png" alt="Funimation spoiler blocker in action" class="img-fluid">

I'll list what exactly it does but it's not doing anything particularly fancy:

- Hide the thumbnail images on the episode select page
- Place an overlay over the video player on page load to hide the spoiler image (click to remove)
- Place an overlay over the episode description box (click to remove)
- Remove the episode title from within the video player itself

Aside: I know Funimation aren't responsible for the episode titles so they're not accountable for the potential spoilers in them. Won't stop me from hiding them though.

Initially I wanted to simply remove the image element that appears before the video plays, but because the video is rendered within an iframe an awful load race is created between the webpage, the iframe, the potential spoiler image within the iframe and even the plugin. Even with hacky methods like spamming a call to the JS .remove() method on the element containing the image would still show the image for long enough to spoil the episode. Because of this I opted for using overlays.

It may not be the most graceful solution but it does exactly what I need it to.

EDIT 13-12-2020: Shortly after making this Funimation stopped showing spoilers in their video splash screens (woohoo). I have also learned that I could do this using userstyles css with the pluging Stylus. Much more lightweight than having a serparate plugin to style each site. 