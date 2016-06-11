---
layout: post
title: GitHub Project Pages and relative links
date: 2016-05-25
author: Lemon
---

GitHub offers free web hosting for each project for jekyll powered sites or just plain static html.  
Unfortunately relative links won't with project pages due to the URL structure.  
This led to broken stylesheets, links and images when I first uploaded this site online.  
As a disclaimer, I'm not a web developer but I thought this might be helpful to some people (i.e. my future self).

By default your project page will be located at:  
**_username.github.io/projectName_**

So when you use a relative link, you'll be expecting it to resolve to:  
**_username.github.io/projectName/images/cat.jpg_**

but instead you'll get:  
**_username.github.io/images/cat.jpg_**

A Google search brings up many different ways to fix this, even the original jekyll theme this site was based on had its own fix.  
I tried a few of them but none of them worked. I suspect this is due to some update to Jekyll or GitHub Pages.

You could always use absolute links instead of relative links but this would mean you wouldn't be able to preview the site locally.

---

## The Fix

Here's a fix that worked, originally found here <https://jekyllrb.com/docs/github-pages/>.  
Why this site wasn't higher up in the search rankings? I don't know.

__Essentially: Add <code class="language-html">{&#123; site.github.url }}</code> to the beginning of all your relative links.__  

__Example: <code class="language-html">&lt;img src="{&#123; site.github.url }}/images/cat.jpg" /&gt;</code>__

This turns all your relative links into absolute links at build time.  
*site.github.url* comes out as blank when building locally so everything remains as a relative link during testing, handy!

## HTTPS

There is one caveat: *site.github.url* returns a http link.  
So your stylesheets still won't load if your website is being served over https.  
I don't think this is likely if you're just hosting on github and you're doing nothing else though.

I use a custom domain and I use Cloudflare for my DNS, who serves content over https.  
In the end, I realised the simplest solution was to just host this site on a subdomain instead. I don't expect this solution to fit the needs of everyone.

From **_tehlemon.com/cute-platformer-blog_**  
To **_cuteplatformer.tehlemon.com_**
