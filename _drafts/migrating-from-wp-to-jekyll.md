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

I havent been updating the blog

## Trapped in Wordpress ecosystem

## Fix your wordpress plugins
the export-jekyll failed with broken zip-files. I was really wondering if the zip-code in the plugin is broken, and I tried to make some fixes into it.

It turned out that one of my own plugins was breaking the zips. I had an empty line after closing php-tags, and that just put some empty space after everything --> zip-files were broken.

Remember not to leave this empty line after closing the tags.
´´´
?>

´´´

## Not even knowing whats broken during the past decade
I have been running wordpress from 2008. In the way I have had multiple broken plugins, different wp-themes, a lot of security holes etc. There's a log of broekn things at this point. 

At this point it feels that the easiest way of fixing this is to migrate to jekyll and go though all md-files with serach on vs code. Fixing this with static sites and seeing which files I have lost during the meny wordpress migrations is nice.

### Runing the blog in few different domains

#### sis files are scatter inside wp-installation
I had lost some of my old downloas while using different versions of the "download-monitor" wp-plugin, and uploading the sis files into various locations of the wp-structure. I manually searched for earch sis-file and fixed the links

### Broken links
using ?p=xxx, and then pages. 
Not using relative urls in every where: 
### All my images are broken
wordpress-migration left same wordpress tags in md-files. Now I have every image with <figure> tags, which are not wkorking with jekyll


´´´
[![supermario world](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg "mario")](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg)
´´´