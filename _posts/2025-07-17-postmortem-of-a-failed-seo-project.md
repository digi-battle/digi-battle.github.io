---
layout: blogpost
title: "Postmortem of a Failed SEO Project"
featured: true
tags: RAMBLING WEB-DESIGN
---

In 2022, I launched a website in the hopes of making some passive income. I'd never tried to monetise a site - everything else I'd made had been a passion project. The result was not... *commercially successful* to put it politely. This is a postmortem of the project, what went wrong and what I learned. 

---

While learning about search engine optimisation and user browsing habits, I noticed a huge number of people in the U.K. were searching for business opening times. Queries like "when does Dumfries Tesco open?" were getting thousands of searches a month. There were already a few sites collating opening times in one place, but I saw space in that market to compete and draw some of this traffic. 

So the plan was set:
1. Collect information about business opening times
2. Display this information in a nice way
3. Put ads on the pages 
4. Become rich

Simple, right?

## Getting the Data

Collecting the data entirely by hand was out of the question. Part of my motivation to start this project was to learn about web scraping and the rules around this. In short, what I learned is:

**LEGALLY:**
1. You must not impede the operation of the server by scraping
2. You must not circumvent anti-bot measures 
3. You must not collect personal data, even if it's available publicly, under protection of GDPR

and **ETHICALLY:**
1. You should check the site's robots.txt file and respect its rules
2. You should read the site's privacy policy and respect their wishes about reproducing their content

Obviously this should not be taken as legal advice so disregard what I've just said - but my point is there are regulations and common courtesies when it comes to scraping. I didn't want to negatively impact any other site with this project, so I followed the rules laid out in each source's robots.txt file, read their terms & conditions, and throttled my queries to a couple per minute (I want to say 5 but I can't remember off the top of my head). No one had an API available to pull this data.

I also avoided any other site that was collating shop opening times as this felt like outright stealing. 

Fun little aside: years later someone made a <a href="https://github.com/stevetoro/digi-battle-crawler" target="_blank">script to scrape the content of my trading card website</a>. I honestly felt flattered that someone would take the time to make something off the back of a thing I made, and the information is there for everyone to do as they please. 

My scaper was a simple C# console application that fed into a SQL database. I used <a href="https://html-agility-pack.net/" target="_blank">HTML Agility Pack</a> and got exposure to <a href="https://en.wikipedia.org/wiki/XPath" target="_blank">XPath</a> for the first time. I had it running day and night for a good while to pull the data I ended up with, and I had to write a different version for each source to query the correct content. 

In the end, I had details of **18,284** businesses for **142** different companies.

## Building the Website

The website was a pretty simple Asp.Net MVC application. The learning curve for me was having SEO at the forefront of the design and structure. 

<a href="https://ahrefs.com/" target="_blank">ahrefs</a> was amazingly helpful for me here. I wasn't even really sure where to start when it came to building for SEO, but their
<a href="https://ahrefs.com/blog/seo-checklist/" target="_blank">SEO Checklist</a> set me on the right path. I had no idea how important site structure was to search rankings, or the impact of URLs, or what metadata was expected with each page. I really can't understate how much I learned from this site. 

Even though I learned a lot, I knew I was still fumbling about in the dark. Still - I felt confident that I was making better choices than I had been when building pages. 

## The Finished Product (minus the ads)

It's certainly not the flashiest website around, but the plan was always to keep it simple and present the information people want as clearly as possible. Function over form. 

![A screenshot of the opening times for RBS bank in Aberdeen](/assets/img/blog/times/rbs-aberdeen.png)

This is an example of a business opening times page that a user would land on from a search engine. 

The design and function can be summarised as this:
- Branch name and today's opening/closing times right at the top. This is what the user is looking for
- Live countdown to the branch's opening/closing
- Table of all business hours for the week, along with a form to fix any errors
- Contact details, address and map using OpenStreetMap.org
- List of businesses in the same area in the same category

Ads would then be loaded between sections using <a href="https://support.google.com/adsense/answer/9261805?hl=en-GB" target="_blank">Google AdSense auto ads</a>.

The site was structured Home > Company Directory > List of Branches > Branch Details.

On the homepage, users were directed to either search by company or location or browse the directory. But I knew that these pages were unlikely to see major traffic as the branch a user is searching for on Google is probably going to be where they land on the site.

## Go-Live & Monitoring

The site went live on 01/06/2022. Now that it was available to the rest of the world I could finally get to grips with some tools for SEO.

### Google Search Console & Bing Webmaster Tools

Honestly, I'd never heard of these before I read the ahrefs SEO checklist. Basically you prove to Google and Bing that you own a website, then they provide data like how many clicks you get on search engine result pages, how many times your site appears in search results, what people are searching for to find your site and a whole load of other stuff. 

They also allow you to submit your sitemap(s) and display which pages have been indexed and (more interestingly) which pages haven't been indexed and why. 

You can then use this information to see what's working, what isn't working, are people able to find your pages, are there keywords that I should be capitalising on etc.

### Google Analytics

Google Analytics wasn't really helpful to me. Maybe I was using it wrong or simply didn't understand enough about the data, but I found the whole system confusing and inconsistent. For example, the *real-time* analytics would show no activity even when I had an active session on the site. Page views were also wildly different to what I was capturing in my internal reporting. There was user activity being reported in GA, but there were too many discrepancies between what was being reported and what I was seeing with my own eyes to trust it.

### ahrefs 

Definitely the most helpful tool for me in terms of optimising my site and learning what not to do. 

The ahrefs Site Explorer shows your keywords, backlinks, referring domains along with comparisons to other websites you're competing with. I'm not doing the service justice but it does a lot more too, even on the free plan.

They also have a Site Audit which I spent a good bit of time using. This crawls your entire site, gives it a health score from 1 to 100 and reports any issues it finds. The issues are broken down into categories and severities and give detailed instructions on how to fix them! This was so incredibly useful to me. I was making my site better while learning what not to do. The issues it reports could be orphan pages, broken redirects, missing or incorrect headers, missing meta tags and so many other things. 

On top of this, it records the number of issues every time you scan and shows changes so you can track issues being fixed or new ones being introduced. 

10/10 would recommend <a href="https://ahrefs.com/" target="_blank">ahrefs</a>.

## Adding Ads

As I've already said, I used Google AdSense auto ads on this site. This dynamically inserts ads on each page based on the structure of the page, which worked pretty well (compared to having to manually create each ad template and then writing them into the page). You can control the volume and style of ads through the admin portal. 

Ads weren't included on launch because I wanted to iron out any teething issues first. So after a month of fixes I rolled out Google Ads in July. 

This wrapped up development of the site!

## Sit Back and Watch the Cheques Roll In, Right?

So now we're done. I have an easy to use website with thousands of pages of information that people want, I've fixed all the issues and followed SEO best practices. The goal was always passive income so now I just wait for my AdSense account to fill up...

**In the first month I received &pound;0.01 in ad revenue.**

This was the first indicator that I'd been terribly naive about this whole thing.

## Cut to the Chase

Not a lot happened after this point besides monitoring the activity. 

Life got in the way in the following years and I didn't have the time or desire to continue working on the site. I reluctantly didn't renew the domain and the site went offline on 18/05/2025. I just couldn't justify the expense. 

During this time the site was seeing 6 figure monthly page impressions, but pages never ranked higher than 4 in search results, and averaged 2.2K page views per day. In the 1,083 days the site was live it received 2,425,889 page views (this excludes error pages, but doesn't factor in bots). 

After almost 3 years, AdSense made &pound;13.74. 

![Google AdSense showing &pound;13.74 balance](/assets/img/blog/times/adsense.jpg)

## What Went Wrong

Someone more in-the-know than me could probably break this down all day long. I'll summarise the main problems and lessons I learned. 

### SEO is not a one-and-done task

I was way too caught up in the dream of passive income. I thought I could invest time working on something for a few months, put it online and it would take care of itself - this simply isn't possible when competing for search engine clicks. Maybe in a market where you dominate the keywords (i.e. no one else is competing or users are searching specifically for the thing that only you provide) this could be possible, but still won't give the best results. 

My site was one of several offering the exact same service and in the time it was live multiple others appeared online. I was in direct competition with a number of other websites, yet I made no effort to maintain relevance or get ahead of the competition. 

To compete in this market you need to regularly review the performance of your site independently (e.g. checking for SEO issues) and comparing it to your competitors (e.g. assessing why their page with the exact same information as your page is ranking higher). 

I can't even plead ignorance because this concept is explained in details by the <a href="https://ahrefs.com/blog/seo-checklist/#periodic-tasks" target="_blank">ahrefs SEO checklist: periodic tasks section</a>. I just didn't do it.

### I didn't research what users actually want

I got the idea for this project by looking at user search engine habits on a site that I can't even find now. This light-bulb moment that happened while doing something else makes up about 50% of my user intent research. The rest was looking at my Google Search Console analytics to see what queries were actually landing users on my site. 

Should go without saying that this simply isn't enough. I never had a grasp on what users were actually looking for when trying to find information about a business. If you don't know what people are looking for then how can you tell them where to find it?

Before I even started working on the site I should have researched what keywords were performing well for websites in the same market. What were competitors doing to land people on their pages. ahrefs has a paid service to do exactly this, but I didn't put my hand in my pocket to produce a better product.

Most importantly, if I had put more time and effort into user research, I would've learned that...

### I was solving a problem that didn't exist 

There are numerous websites collecting business opening times, and I sincerely hope that they're doing well and making money, but Google already provides opening times before users ever lay eyes on your site.

![Google search engine results page showing the opening times for a business before any search results](/assets/img/blog/times/google-serp.jpg)

If you ask Google when a business opens it can almost always provide an answer. This appears right at the top of the search engine results page before any other site that has this information. Google collects this information from:

- Business Profile users (businesses provide their information directly to Google for exactly this purpose)
- Analysing Google Maps and review data 
- Even **crawling websites that have this information already**

I witnessed this last one myself recently when I searched for a small business local to me and Google was able to show me the hours listed on the company's site, without going to the site myself.

I didn't know this was a feature at the time because DuckDuckGo was my default search engine... More evidence of my lack of research.

Yes, you'll only see this if you're using Google, but at the time of writing this Google has a 93.35% market share for search engines. Meaning that 93/100 people looking for opening times will get their question answered without going to any other website. The subset of people who either didn't use Google to see that answer, or simply didn't trust it, then have to choose between my site or at least 5 others to get what they want. 

Getting clicks felt like fighting over crumbs. 

## In Conclusion

The website may have been a *commercial* failure, but I don't see it as a personal one. 

I got exposure to so many new technologies and walked away with a better understanding of how the Internet works and what goes in to an online business. 

I don't regret the time I spent working on it even if I have nothing tangible to show for it. I have fond memories of staying up ridiculously late working on my web scraper and watching it run while I played video games. Going about my daily business and thinking about how I'm going to build a feature of the site or structure something in the database when I got home. My life is so busy now and this project captures a time in my life when I could fully indulge in something I'm passionate about without thinking about anything else. 

Because of this project, I feel better equipped to succeed in the next idea that I have. And I'm not afraid to try again. 

---

I'll leave you with some tidbits of mildly interesting data.

- The most popular shop was Liverpool Costco, which was viewed 12690 times
- Traffic spiked massively around holidays and Christmas time
- 12 users were kind enough to submit corrections to the times stored on the site
- The contact form was submitted 802 times, all of which was spam. I intentionally didn't put a Captcha or any anti-bot checks on the form because I was curious about what kind of junk the form would receive. I might write up a separate post digging into these
- Google search console has removed my access to any information about the domain, including historic reports. But Bing Webmaster Tools is still showing me search performance data even though I haven't owned the domain for months 
