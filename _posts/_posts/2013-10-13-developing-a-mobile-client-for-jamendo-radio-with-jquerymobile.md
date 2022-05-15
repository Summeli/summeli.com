---
id: 4579
title: 'Developing a mobile client for Jamendo Radio with jQueryMobile'
date: '2013-10-13T15:15:08+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4579'
permalink: /4579/
categories:
    - 'Web Development'
tags:
    - android
    - bb10
    - firefoxos
    - html5
    - ios
    - jquery
    - jQueryMobile
    - tizen
---

In this article I’m going to create a jQueryMobile based client for Jamendo Radio.  
The JQuery Mobile based UIs can be run on almost every smartphone platform; iOS, Android, Windows Phone, BlackBerry10, Tizen, Firefox OS etc. The development of JQuery Mobile based UIs is very nice, since you can develop them with HTML and JavaScript in a standard desktop browser.  
Here’s a short video of JamendoFM running on FirefoxOS.  

<iframe allowfullscreen="" frameborder="0" height="315" loading="lazy" src="//www.youtube.com/embed/OnXUEeg31JY" width="420"></iframe>

### Getting the API for Jamendo

At first you must register to <http://developer.jamendo.com/> to get the API key for creating a client for Jamendo API.

### Creating the UI with HTML pages

The first page will be used for listing the radio mixes form Jamendo.com.

```
<!-- Starting page, listing the mixes -->
<div id="radioListPage" data-role="page">
<div data-role="header" data-position="fixed">
<h1>JamendoFM</h1>
</div>
<!-- /header -->
<div data-role="content">
<ul id="radioList" data-role="listview" data-inset="true"></ul>
 <a href="index.html#aboutPage" data-role="button">About</a></div>
<!-- /content --></div>
<!-- /page -->
```

The radio list will be loaded into the radioList-element. The next step is to populate the radioList with jQuery.  
The data is loaded with [JSONP ](http://en.wikipedia.org/wiki/JSONP)so the extra parameter &amp;callback=? is added to the end of the requests.

```
$( document ).delegate("#radioListPage", "pagebeforeshow", function()  {
   $.mobile.loading( 'show',{text:'loading'} );
   var jqxhr = $.getJSON('http://api.jamendo.com/v3.0/radios?client_id='+g_clientId+'&callback=?', null, null,'application/json')
   .done(function(result) {
      radioListPageLoaded=true;
      console.log(result);
      $.mobile.loading( 'hide' );
      var list = $("#radioList").listview();
      $(result.results).each(function(index){
         $(list).append('<li><a href="index.html#radioPage" onclick="sessionStorage.radioId=' + this.id+ '">'
           + '<img src="'+this.image+'" class="ui-li-icon"/> <h3>' + this.dispname + '</h3></a> </li>');
      });
      $("#radioList").listview('refresh');
   })
   .fail(function() {
     radioListPageLoaded = false;
     jQuery.mobile.changePage("#errorPage");
     });
};
```

The second page will be for listening the radio. In this page we’re going to show the pageCover, and load the audiostream with HTML5 audio-tags.

```
<!-- Radio Listening page -->
<div id="radioPage" data-role="page" data-add-back-btn="true">
<div id="radioHeader" data-role="header"></div>
<!-- /header -->
<div data-role="content"><img id="trackcover" alt="" src="img/tempcover.png" />
<div id="artist"></div>
<div id="album"></div>
 <audio id="radiocontrols" width="300" height="32" controls="controls"><source src="http://streaming.radionomy.com/JamLounge" type="audio/ogg" />
            </audio></div>
<!-- /content --></div>
<!-- /page -->
```

In the javavascriptside, we’re going to use jQuery to fill in the radioHeader, and replace the audio-src and the src for the cover art.  
The radioHeader can be simply added with

```
 $('#radioHeader #radioName').text(result.results[0].dispname);
```

The radiosource can be set(replaced) like this:

```
function setRadioStream(sourceUrl) {
    var audio = $("#radiocontrols");
    $("#radiosource").attr("src", sourceUrl);
    /*let's play the audio*/
    audio[0].pause();
    audio[0].load();
    audio[0].play();
};
```

### Adding page transition effects

Adding pagetransition effects with jQueryMobile is easy. Just add data-transition=”slide” argument to the link-elements like this:

```
<a href="index.html#aboutPage" data-transition="slide" data-role="button">About</a>
```

### JamendoFM in Github

You can find the JamendoFM client at github: [**https://github.com/Summeli/JamendoFM**](https://github.com/Summeli/JamendoFM)

### PhoneGap

I’m using [Phonegap](http://phonegap.com/) to package my application to multiple platforms such as Android, BB10 etc.  
Unfortunately the Windows Phone can not stream ogg vorbis though html5 audio tags, so there will be no Windows Phone client, but creating one with PhoneGap would be easy.

### Porting JamendoFM to other HTML5 platofrms

In later posts I’m going to use JamendoFM as an example project how to port/create jQueryMobile based applications for Tizen and FirefoxOS.