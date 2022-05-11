---
id: 4961
title: 'Green Screen Magic for Windows Phone'
date: '2014-01-28T23:36:26+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4961'
permalink: /4961/
categories:
    - 'Windows Phone Development'
tags:
    - greenscreen
    - 'windows phone'
---

Developer.nokia.com organized another Imaging challenge for developers. This time I decided to play with the chroma key and I created two Green Screen applicatons. You can find my article from Nokia wiki: [Green\_Screen\_Magic(Chroma\_Key)\_with\_Nokia\_Imaging\_SDK](http://developer.nokia.com/community/wiki/Green_Screen_Magic(Chroma_Key)_with_Nokia_Imaging_SDK)  
*Green Screen Helper*, an app to help users set up a high quality green screen in preparation for Chroma Key photography. The application uses the chroma key filter in real time to make a selected colour black – enabling the user to see which parts of the screen will not be properly filtered when applying the chroma key filter. This is helpful, since it then becomes easy to see where the editing scene needs to be fixed – by adjusting the lights, or fixing wrinkles. In addition, the hue range sensitivity accepted by the filter can be adjusted: a broader hue range will be more tolerant of poor lighting and wrinkles in the background, but may result in some of the subject also being selected.  
  
<iframe allowfullscreen="" frameborder="0" height="315" loading="lazy" src="//www.youtube.com/embed/6zQCphMTGcI" width="560"></iframe>  
  
The other application is called *Green Screen Magic*, it’s a simple photo editing app which will replace the green screen area with a background. This app uses the same approach as the previous app to help the user to select the chroma key, and adjust sensitivity. After that it uses the blend functionality to combine two images.  
  
<iframe allowfullscreen="" frameborder="0" height="315" loading="lazy" src="//www.youtube.com/embed/3SLm4Pi29Zg" width="560"></iframe>