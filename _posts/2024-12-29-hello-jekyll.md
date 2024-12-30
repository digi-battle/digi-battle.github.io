---
layout: blogpost
title: "Hello Jekyll"
---

Welcome to my new personal site built with Jekyll!

I've been wanting to update my website for a while, mainly to make it easier to publish content and things I've been working on. The old site was a simple PHP template I made that served static HTML content. This meant I had to be at my development PC to be able to write or publish anything, but I'm so on-the-go these days that finding time to sit down at my PC is rare. 

Here's what I was looking for in a new site:
1. Some way to write blog posts / ramblings from anywhere, even my phone
2. An easy way to add things I've been working on, which may be standalone HTML pages inconsistent with the rest of the site
3. A deployment method that's not a complete headache

At first I went to <a href="https://umbraco.com/" target="_blank" rel="noopener">Umbraco</a>. I'd used Umbraco professionally about 5 years ago and wanted to refamiliarise myself with it. A lot has changed since I last used it. 

Umbraco is a fully-featured CMS built on .NET. It would let me login to the backend to create new posts from anywhere. However, adding example work in HTML files is a headache and would mean I'd need to create new templates and document types for each new page I wanted to add before even adding the page itself. There was also the pain of keeping up to date with security patches and updates (not to mention updates for plugins) that naturally comes with hosting a third-party application. 

I wasn't put off Umbraco, but I stumbled across <a href="https://jekyllrb.com/" target="_blank" rel="noopener">Jekyll</a> and choosing it was a no-brainer.

I hadn't considered using a static site generator. I used one in the past but it was clunky and horrible and required a lot of work&hellip; but that was probably because I built it myself. It used XML to store the data for posts and static HTML files to build the layouts for each page. But Jekyll is everything my site generator was and SOOOOO much more.

With Jekyll I can just dump markdown or HTML files into the correct folder (whether it's a post or a rambling or whatever) and Jekyll takes care of the rest. Because of the way layouts are defined it's also so much easier to restyle the entire website should I redesign it. The data still exists in their own files ready to be loaded in whatever way I choose.

So that takes care of my first 2 problems. Deployment is handled by <a href="https://pages.github.com/" target="_blank" rel="noopener">GitHub Pages</a>. GitHub has built in support for Jekyll so all I need to do is commit my changes to the main branch of this site's repo and it will automatically re-compile the site and deploy it. Simple.

And that's it! I can see myself using Jekyll for a good while and I'm happy for now. If that changes I'll be sure to write about it. 