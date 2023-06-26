---
id: 12035
title: 'Configuring SyntaxHighlighter plugin to StripBrs'
date: '2018-12-03T10:21:35+02:00'
author: Summeli
layout: post
guid: 'https://www.summeli.com/?p=12035'
permalink: /12035/
categories:
    - 'Web Development'
    - WordPress
tags:
    - javascript
    - php
    - WordPress
    - wp
---

I had way too much trouble with the new version of the SyntaxHighlighter Evolved plugin. The default configuration page is missing the option to StripBrs. A quick and dirty solution was to write a plugin to configure the other plugin.  
The SyntaxHighlighter configuration is easy. The plugin is running on JavaScript, so all we have to do is to

```
SyntaxHighlighter.config.stripBrs = true;
SyntaxHighlighter.all();
```

To get there I wrote a simple plugin that add the new js after WordPress js scripts. Here’s how it’s done:

```
function add_js_config() {
    wp_register_script( 'syntaxhighlighter_config',
                       plugins_url('syntaxhighlightstripbrs.js',__FILE__),
                       array('jquery','syntaxhighlighter'),
                       '1.0',
                       true);
    wp_enqueue_script('syntaxhighlighter_config');
}
add_action( 'wp_enqueue_scripts', 'add_js_config' );
```

The plugin can be found from github: <https://github.com/Summeli/SyntaxHighlight-StripBrs>