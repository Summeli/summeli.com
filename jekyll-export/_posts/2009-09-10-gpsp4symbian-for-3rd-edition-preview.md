---
id: 1181
title: 'gpSP4Symbian: S60 3rd edition preview'
date: '2009-09-10T20:24:49+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1181'
permalink: /1181/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
categories:
    - 'S60 3rd edition'
tags:
    - gpsp
    - N95
---

This is just an initial release to gain some feedback how the port is currently working. I would like to know if you get any games running at correct speed. The first number in the fps-counter is telling how fast the emulator is running( it should be 60). If you do get something running at that speed, please also test the audio then. I have some tricks planned for the audio, but there’s really no point of doing it, if it doesn’t run fast enough.  
Please list some games in the comments that you got running well, so I can test the audio with those. It’s really no point of tweaking audio, if the game doesn’t run well. Tell also what phone you are using. It would be very interesting to have some results from phones with 600Mhz ARM processor.  
![](/wp-content/uploads/2009/09/gba.jpg)  
**Know issues:**

- key config is missing
- only one game can be loaded with each run
- audio may not work well. I really didn’t have a good setup to test it.
- You should turn audio on after a game has been loaded. Turning the audio on before loading the game will crash the emulator.
- The emulator requires a lot of CPU power. It really doesn’t work with my N96 or N73

**KEYCONFIG**  
There is no keyconfig yet available, so you’ll have to bear with these for a while. up/down/left/righ form the d-pad  
4: L  
5: A  
6: start  
7: R  
8: B  
9: select  
\#: save state  
\* :load state  
left softkey: menu  
  
**Installation**  
Install the emulator from the sis file, and then place the following files under E:\\GBA folder

- game\_config.txt  
    You should find this file with the installation package
- gba\_bios.bin  
    You should find this on your own. Please **don’t post links to this file in the comments.** Make sure to get an authentic one, it’ll be exactly 16384 bytes large and should have the following md5sum value: a860e8c0b6d573d191e4ec7db1b1e4f6
- put also ROM’s under E:\\GBA folder

Also Nokia’s OpenC plugin is required. So if you don’t have it, then you should install it asap.  
And now you’re done. Have fun! 😉  
**Credits:**  
This emulator is based on gpsp originally written by Exophase. It also uses SDL port by Anotherguest. Symbian porting was made by me, Summeli.  
**Download**  
**[ gpsp4Symbian\_v01.sis (7403 downloads) ](http://summeli.com/download/11248/ "Version 0.1")**  
\[ad\]  
**Sources**  
This is my first github project. Get my sources from [http://github.com/Summeli](http://github.com/Summeli/gpSP4S60)  
**Compatibility**  
1\. Spiderman – battle for new york (blue screen).  
2\. Tekken advance (perfect).  
3\. Street fighter – zero 3 upper (perfect)  
4\. Disney magical quest starring mickey and minni (perfect)  
5\. Dragonball Z – transformation (blue screen).  
6\. Manic miner. (perfect).  
7\. Harlem globetrotters – world tour (perfect).  
8\. Super mario circuit. (perfect).  
9\. Column Crown (perfect)  
10\. Chu chu rocket (perfect)  
11\. Disney piglet big game. (perfect).  
12\. Disney sport skateboarding. (perfect).  
13\. Denki blocks. (perfect).  
14\. Disney extreme skate adventure. (perfect).  
15\. Kim possible. (perfect).  
16\. Dora the explorer – super star adventure. (perfect).  
17\. Dexter laboratory – chess chalenge (perfect).  
18\. Deal or no deal. (perfect).  
19\. Dogz. (perfect).  
20\. Dora the explorer – the search for pirate pig treasure (perfect).  
21\. Dr.muto (bluescreen but when play perfect).  
22\. Disney – the jungle book. (perfect).  
23\. Demon driver – time to burn rubber. (bluescreen but when play perfect).  
24\. Dr.mario. (perfect).  
25\. Cartoon network – block party.  
26\. Chessmaster. (perfect).  
27\. Dragon quest – monster caravan heart. (perfect).  
28\. Cartoon network – block party. (perfect).  
29\. Yggdra union – we’ll never fight alone. (perfect but can’t save the game).  
30\. Aggasi Tennis Generation (perfect).  
31\. Super monkey ball Jr. (blue screen).  
32\. Cabbage patch kid – the patch puppy rescue (perfect).  
33\. Cabella’s big game hunter (bluescreen).  
34\. Caesar palace advance – millenium gold edition.  
35\. Camp lazio – leaky lake games. (perfect).  
36\. Candy land chutes and ladders – original memory game.  
37\. Capcom classic – mini misx. (perfect).  
38\. Car batler joe. (perfect).  
39\. Need for speed underground 2 (blue screen).  
40\. Ultimate spiderman (bluescreen and when play it perfect).