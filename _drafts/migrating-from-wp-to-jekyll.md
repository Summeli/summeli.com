---
layout: post
title:  "Migrating from Wordpress to jekyll!"
author: Summeli
categories:
    - wordpres
    - jekyll
tags:
    - porting
---

I haven't been updating the blog for a while. I've been too busy doing other things. The fact is that wordpress needs constant care to keep it running well. 

### Trapped in Wordpress ecosystem.
I also felt trapped in Wordpress ecosystem. Some plugins stop working when the authors don't update them anymore, or they go behind subscription fees, which is ok. But I only want to write blog posts few times a year.

I also have been jumping between different web-hotels (2008, remember) and between different cloud vendors inside docker containers. Hosting a blog is still quite a bit of work, and those servers are not free.

#### Jekyll to the rescue
The Jekyll seems like an optimal product for me. Blogging with Markdown documents, and running them on github for free. This all sounds too good to be true. 

Before migrating into Jekyll, I read some blogs post about it "I've been using wordpress for three months and it was not for me. Here's how I migrated into Jekyll".

Well. I have been running this blog since 2008, and I have 180 post. I wonder how easy this is going to be...

## Migration to Jekyll

### Fix your wordpress plugins
the export-jekyll failed with broken zip-files. I was really wondering if the zip-code in the plugin is broken, and I tried to make some fixes into it.

It turned out that one of my own plugins was breaking the zips. I had an empty line after closing php-tags, and that just put some empty space after everything --> zip-files were broken.

Remember not to leave this empty line after closing the tags.
´´´
?>

´´´

### Not even knowing what's broken during the past decade
I have been running wordpress from 2008. In the way I have had multiple broken plugins, different wp-themes, a lot of security holes etc. There's a log of broekn things at this point. 

At this point it feels that the easiest way of fixing this is to migrate to jekyll and go though all md-files with serach on vs code. Fixing this with static sites and seeing which files I have lost during the meny wordpress migrations is nice.

### Runing the blog in few different domains

#### sis files are scatter inside wp-installation
I had lost some of my old downloas while using different versions of the "download-monitor" wp-plugin, and uploading the sis files into various locations of the wp-structure. I manually searched for earch sis-file and fixed the links. So now all of my symbian sis files (which I served here) can be found!

### Broken links
using ?p=xxx, and then pages. 
Not using relative urls. This was a mistake, and I regret it. Jekyll is very good at reading relative links, and checking that those links / files are found in the site. So I have to fix all links to my blog by hand.

Here's a best case scenario image link, which I have to covert into relative urls.
´´´
[![supermario world](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg "mario")](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg)
´´´

### All my images are broken
wordpress-migration left same wordpress tags in md-files. Now I have every image with <figure> and all kinds of "wp-gallery" html-tags, which are not working with jekyll. So I need to clean up all references to images by hand.

## Everything is fixed
NICE! I can finally blog with Jekyll and MD files. I love it.
