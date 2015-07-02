---
layout: post
title: "I wrote my email address in Nethack"
date: 2014/08/12
categories: nethack
---

<img src='{{ site.url }}/assets/nethack-email-only-email.png' alt='my email made of Nethack monsters' title='my email made of Nethack monsters' />

Yes, this is a screenshot of my email address, made of Nethack monsters. That was fun!

A few things to note, if you ever want to do this:

- Don't use a corridor; use an empty room. I didn't realize that I wouldn't be able to create a monster with the symbol `.` until it was too late.
- There aren't any infravisible monsters in the `m` or `M` classes, so that was a problem. I just had to use an `n`.

And here are the (very patchy) notes I took while doing this:

    Steps to do the magicness:
    1. Start as an elven wizard
    2. #levelchange 30
    3. Find a nice long corridor / area to put the email (use blessed magic mapping if you want)
    4. Drop all your current stuff somewhere out of the way
    5. Wish for (then Ctrl+I):
      - WEAPONS / ARMOR (wield / wear all of these)
      - a blessed +50 weapon of your choice (not Stormbringer, ex. Frost Brand) (for killing things, #enhance if desired)
      - blessed fixed +25 gauntlets of power (carrying more stuff and AC)
      - blessed fixed +25 speed boots (being fast of course, AC)
      - stuff like SDSM / CoMR / etc. if desired
      - SCROLLS / POTIONS / RINGS (put them on) / WANDS / AMULETS (put them on)
      - 10 blessed scrolls of earth (for sealing off an area)
      - 2 blessed scrolls of genocide (for clearing existing monsters)
      - blessed ring of slow digestion (for convenience, not required, but makes tele easier)
      - blessed amulet of ESP (for seeing monsters)
    5. Genocide * to get rid of stray monsters
    6. Use the scrolls of earth to seal off your area (with the exact length of your email); zap bad boulders with starting force bolt and move the rocks somewhere else
      - You may have to use more complicated methods like jellies if you're planning to use something like H in your email, or just locate strategically
    7. Go to the beginning of the text area (i.e. @######)
    8. Genocide * again just to be safe
    9. For each letter / monster you have in your email before the @:
    a. Can it be tame?
    yes: Ctrl+G tame &lt;your letter or monster&gt;, move right to displace it
    no: move right, Ctrl+G peaceful &lt;thingy&gt;, if it appeared on the wrong side then kill it and try again
    b. Rinse and repeat. If the monster moves while you're trying to create the next one, just wait for them to all line up again.
    10. For each letter / monster you have in your email after the @:
    a. Ctrl+G it until it eventually ends up in the spot you want (this takes no in-game time)
    11. Enjoy

I didn't end up needing the weapon and the AC, but it's always fun to be overprepared. :D

By the way, here's a screenshot of the entire map, if you're wondering:

<img src='{{ site.url }}/assets/nethack-email-entire-map.png' alt='the entire map' title='the entire map' />

Yeah, copy/paste helps.
