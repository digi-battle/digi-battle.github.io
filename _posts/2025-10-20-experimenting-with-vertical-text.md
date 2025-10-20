---
layout: blogpost
name: "Experimenting with Vertical Text"
tags: CSS WEB-DESIGN
---

![Fed.gif](/assets/img/blog/vertical-text/fed.gif)

<p style="text-align: center;">
	(<a href="/work/vertical-text">check it out</a>)
</p>

I've been playing around with a few different design elements, namely vertical text, justified text, sticky elements and flex. 

I used these elements to create [this page](/work/vertical-text).

Vertical text is achieved using ```text-orientation: upright;``` in most cases. I also did this by setting ```width: .9rem;``` in others places to force the word to wrap onto multple lines, breaking on each character. 

I went with [Delta Gothic One](https://fonts.google.com/specimen/Dela+Gothic+One) for the font. I love how bold and heavy it is and I wanted to play around with Japanese text, which this font supports. The overall blockiness of the type looks really nice vertically and in longer, mixed-case justified paragraphs.

Also learned about outlining text with ```-webkit-text-stroke: 3px white;```. 

I was influenced by the packaging of KMC Perfect Fit Card Sleeves:
![KMC Perfect Fit Card Sleeves](/assets/img/blog/vertical-text/kmc.jpg)

And the cover of The Amazing Spiderman issue 300:
![The Amazing Spiderman issue 300 cover](/assets/img/blog/vertical-text/spiderman.jpg)

This was really just a little experiment to play around with different ideas I hadn't explored before, nothing to write home about. But it was fun putting everything together. I'm not too satisfied with the fixed-right vertical elements nor the vertical text in English. I feel Japanese Katakana is much more visually appealing than English when vertical. But I'd definitely like to play around with sticky elements again. 

Further reading:
- [https://developer.mozilla.org/en-US/docs/Web/CSS/text-orientation](https://developer.mozilla.org/en-US/docs/Web/CSS/text-orientation)
- [https://kinsta.com/blog/css-text-outline](https://kinsta.com/blog/css-text-outline/)