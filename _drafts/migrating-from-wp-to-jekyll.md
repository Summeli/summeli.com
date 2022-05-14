---
layout: post
title: "Migrating from Wordpress to jekyll!"
author: Summeli
description: Migrating from Wordpress to Jekyll.
categories:
    - wordpres
    - jekyll
tags:
    - porting
---

I've been running this blog since 2008, but I haven't been updating the blog for a while. I've been too busy doing other things. The problem is that Wordpress needs constant care to keep it running well.

### Trapped in Wordpress ecosystem

I also felt trapped in Wordpress ecosystem. Some plugins stop working when the authors don't update them anymore, or they go behind subscription fees, which is ok. But I only want to write blog posts few times a year.

I also have been jumping between different web-hotels (2008, remember) and between different cloud vendors inside docker containers. Hosting a blog is still quite a bit of work, and those servers are not free. 

#### Jekyll to the rescue

The Jekyll seems like an optimal product for me. Blogging with Markdown documents, and running them on github for free. This all sounds too good to be true.

Before migrating into Jekyll, I read some blogs post about it "I've been using wordpress for three months and it was not for me. Here's how I migrated into Jekyll" Well. I have been running this blog since 2008, and I have 180 post. I wonder how easy this is going to be...

## Migration to Jekyll

I instelled Wordpress to Jekyll wordpress plugin and started the jorney. The idea was that I would get nice Markdown documents from the blog that would be easy to maintain in the future. 

### Fix your wordpress plugins

The export-jekyll pluging failed with broken zip-files. I was really wondering if the zip-code in the plugin is broken, and I tried to make some fixes into it.

It turned out that one of my own plugins was breaking the zips. I had an empty line after closing php-tags, and that just put some empty space after everything --> zip-files were broken.

Remember not to leave this empty line after closing the tags.   

´´´   
?>

´´´    

### Not even knowing what's broken during the past decade

I have been running wordpress from 2008. In the way I have had multiple broken plugins, different wp-themes, a lot of security holes etc. There's a lot of broken things at this point.

It feels that the easiest way of fixing this is to migrate to Jekyll and go though all Markdown files with search-tool on VsCode. Fixing stuff withing static files after the migration sounds like a solid plan.

### Runing the blog in few different domains

I have been running the blog in few diffrent domains: "koti.kapsi.fi/summeli", "summeli.fi" and now "summeli.com". These migrations have also left a mark. For some reason I had absolute url's everywhere, which was also a problem, since I have tools to only check relative links that the link still exists. I converted all of my absolute urls (some were broken) into relative ones.

#### Sis files are scatter inside wp-installation

I had lost some of my old symbian downloas while using different versions of the Download-Monitor wp-plugin, and uploading the sis files into various locations of the wp-structure. I manually searched for earch sis-file and fixed the links. So now all of my symbian sis files (which I have ever served here) can be found!

### Broken links

Not using relative urls. This was a mistake, and I regret it. The Github workflow has a static check for links, which is very good verifying that those links / files are found in the site. So I have to fix all links to my blog by hand.

Here's a typical image link, which I have to covert into relative urls.
´´´
[![supermario world](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg "mario")](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg)
´´´

I had to change these into.
´´´
[![supermario world](/jekyll-export/wp-content/uploads/2008/09/mario.jpg "mario")](/jekyll-export/wp-content/uploads/2008/09/mario.jpg)
´´´

### All my images are broken

Wordpress migration left same wordpress tags in md-files. Now I have every image with and all kinds of "wp-gallery" html-tags, which are not working with Jekyll. So I need to clean up all references to images by hand.

### What about comments

Moving the coments into Discuss seemd like the easiest way of keeping them, so I just updaloaded them into there, and configured then back on. This was the easies part of the whole migration.

## Everything is fixed

NICE! I can finally blog with Jekyll and MD files. I love it.
