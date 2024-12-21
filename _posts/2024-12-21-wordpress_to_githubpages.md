---
layout: post
permalink: /wordpress_to_githubpages/
title: Moved my Worpress Blog to GitHub Pages
date: 2024-12-21
publish: true
categories: [migration, github-pages]
tags: []
---

### Moving Developer Playground to GitHub Pages

I'm excited to announce that Developer Playground has moved from [developerplayground.net](http://developerplayground.net) to its new home: [https://stfnjstn.github.io/developerplayground](https://stfnjstn.github.io/developerplayground).

This change was driven by several factors. When the hosting prices for my WordPress blog recently doubled, I realized that continuing with that platform wasn't sustainable given my infrequent posting schedule. Although I don’t have a lot of time to blog, it’s important to me to preserve my past work and improve my presence online. With this migration, I hope to use the blog more actively, especially to showcase my apps and games.

During the migration process, I discovered unexpected challenges. Exporting my WordPress content revealed multiple rendering issues, such as unclosed formatting tags and inconsistencies that weren’t visible in the WordPress editor. These issues made me appreciate the simplicity of Markdown files and the Git-based approach offered by Jekyll and GitHub Pages. By working directly with Markdown, I’ve achieved a more consistent look and feel for my blog.

#### Migration Steps

Here’s a quick summary of the steps I followed to migrate my blog:

1. **Export WordPress Content**: I used WordPress's built-in export tool to download an XML file of my posts and pages.
2. **Convert to Jekyll**: I utilized [WP2Jekyll](https://github.com/seanthegeek/wp2jekyll), a handy tool for converting WordPress exports into Jekyll-compatible Markdown files.
3. **Fix Links and Images**: The exported content needed manual corrections for links and images to align with the new structure.
4. **Create the Repository**: I set up a new repository on GitHub for the blog.
5. **Enable GitHub Pages**: I configured the repository to use GitHub Pages and published the site.

The most time-consuming part of the process was resolving the inconsistencies in the exported posts. Once complete, everything was ready for publishing.

#### Why GitHub Pages?

Unlike WordPress, GitHub Pages focuses on static site generation, which aligns perfectly with my needs. While WordPress offers a feature-rich editor and plugin ecosystem, GitHub Pages allows full control over the site's content and appearance using simple Markdown files. It’s a trade-off between convenience and flexibility, and for me, the latter wins for this project.

I’m looking forward to sharing more updates on Developer Playground and making better use of this new platform. Check it out at [https://stfnjstn.github.io/developerplayground](https://stfnjstn.github.io/developerplayground), and stay tuned for more content!

Cheers
Stefan
