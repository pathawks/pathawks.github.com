---
layout: post
hide: True
math: True
title: Random Bug
---
I seem to have stumbled accross a very strange bug.

When I was in middle school, I very much enjoyed writing "screen savers" for my computer. I had an old (even at the time) DOS box in my room, and anything I could do to make it more Mac like was generally a positive. I once even when at far as writing a little program that would play the intro to Aerosmith's _Sweet Emotion_ each time the computer booted up. That little program and accompanying audio data took up a substancial chunk of my computer's 20Mb hard drive.

But we're getting off track.

So one such "screen saver" that I wrote in **[ASIC](http://asic.pathawks.com/)** (Almost BASIC), would paint the screen with overlapping colored boxes. I need to put "screen saver" in quotes because the program never cleared the screen and never painted a black or grey pixel, so I doubt very much that it would do anything to prevent [burn in](http://en.wikipedia.org/wiki/Screen_burn-in).

Anyway, I recently found the code to this program (Thanks Dad for holding onto it for so many years.) and, running it inside of [**DOSBox**](http://www.dosbox.com/), I have discovered something quite odd.  
Not only does the program output the same pattern every time it's run, but after a short amount of time, it falls into a loop.  
The loop seems to repeat about every 13 seconds.

Notice the box towards the top right of the screen that goes from purple to green to purple to green....

<iframe width="640" height="480" src="http://www.youtube-nocookie.com/embed/RucsIOZPpvI?rel=0" frameborder="0" allowfullscreen="allowfullscreen" style="margin:1em auto;">
</iframe>


I'm not sure if this is a problem with my program itself, with the **ASIC** compiler, or with **DOSBox**.  
Any advice on how to diagnose this problem would be much appreciated.


        CLS
        RANDOMIZE
        SCREEN 9
        
        RESTART:
        GOSUB BIGI:
        REDOX:
        X = RND(0)
        IF X > 320 THEN REDOX:
        
        REDOY:
        Y = RND(0)
        IF Y > 620 THEN REDOY:
        
        RECOL:
        COL = RND(0)
        IF COL > 15 THEN RECOL:
        IF COL = 0 THEN RECOL:
        IF COL = 8 THEN RECOL:
        
        Z = Y
        FOR N = 1 TO 23
        FOR E = 1 TO 23
        PSET (X, Z), COL
        Z = Z + 2
        NEXT E
        Z = Y
        X = X + 2
        NEXT N
        
        G$ = INKEY$
        IF G$ = "" THEN RESTART:
        SCREEN 0
        END
        
        
        BIGI:
        FOR A = 283 TO 335
        PSET (A, 628), 7
        PSET (A, 578), 15
        NEXT A
        
        FOR B = 578 TO 628
        PSET (283, B), 7
        PSET (335, B), 15
        NEXT B
        
        FOR C = 295 TO 322
        PSET (C, 603), 15
        NEXT C
        
        FOR D = 588 TO 618
        PSET (295, D), 7
        PSET (322, D), 15
        NEXT D
        
        RETURN

The first thing I noticed about this (aside from the lack of BASIC syntax highlighting in any modern editor) is just how inefficient I was being with random numbers. The **ASIC** [**RND** command](http://asic.pathawks.com/reference/rnd) returns a number between 0 and 32767 ($2^{15}-1$). A thinking person would divide this number by the limit of the desired range and use the remainder. I simply discarded 99% of the generated numbers and told the computer to try again. This could result in simply exhausting the supply of random numbers. Right now, this is my best guess about what's happening.

I cannot be sure if this is just a **DOSBox** thing or an **ASIC** thing.

We can avoid these problems (and make the program really sing) with just a few changes.

        RANDOMIZE
        SCREEN 9
        
        RESTART:
        FOR L = 0 TO 1000
        X = RND(0)
        X = X MOD 320
        
        Y = RND(0)
        Y = Y MOD 620
        
        COL = RND(0)
        COL = COL MOD 16
        
        Z = Y
        FOR N = 1 TO 23
        FOR E = 1 TO 23
        PSET (X, Z), COL
        Z = Z + 2
        NEXT E
        Z = Y
        X = X + 2
        NEXT N
        
        G$ = INKEY$
        IF G$ <> "" THEN ENDPROGRAM:
        NEXT L
        SCREEN 9
        GOTO RESTART:
        
        ENDPROGRAM:
        SCREEN 0
        END
        
<iframe width="640" height="480" src="http://www.youtube-nocookie.com/embed/trVBm6geLYE?rel=0" frameborder="0" allowfullscreen="allowfullscreen" style="margin:1em auto;">
</iframe>
