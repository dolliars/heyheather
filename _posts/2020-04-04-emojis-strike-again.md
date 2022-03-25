---
layout: post
title:  "Emojis strike again"
date:   2020-04-04 03:08:17 -0500
categories: [dwm, Xorg, fonts, emojis ]
---

I thought you might find the current lepidoptera that I've come across
interesting. I haven't figured out where its habitat is but I have observed some
of its behavior. My first observation was that dwm "crashed", and when it did I
saw the following message: 

```
dwm: fatal error: request code=139, error code=16
X Error of failed request:  BadLength (poly request too large or internal Xlib length error)
  Major opcode of failed request:  139 (RENDER)
  Minor opcode of failed request:  20 (RenderAddGlyphs)
  Serial number of failed request:  28741
  Current serial number in output stream:  28748

  xinit: connection to X server lost waiting for X server to shut down (II)
  Server terminated successfully (0) Closing log file
```

I found [this forum thread][forum-thread-1] of someone who had pretty much the
exact same problem. It seems the problem isn't with dwm(?), but something is
making X exit. As [others][issue-dwm] [have noted][forum-thread-2] it seems to
be an issue with emojis. I first noticed this when I clicked on a twitter
account that had emojis in their name. Right after clicking on the profile
fitting that criteria, I'm booted out and get the messages stated above.
Another weird thing is the fact that it seems to be with specific emojis. I
looked up "magnifying glass emoji" and there are two: left-pointing and
right-pointing. When I go to a page with the left-pointing magnifying glass,
everything is fine. But when I go to a page with the right-pointing magnifying
glass, my system is having none of it. Another particularity of this bug is that
I can still google it and I can still see right-pointing magnifying glass in the
search result page for instance. But once I click on the page X closes. These
are the few emojis I tested in different places: [test 1][test-1], [test
2][test-2], [test 3][test-3].

As I've been thinking about this problem, explaining it and dealing with it, I
realized that the issue seems to be when a particular emoji is in the title of a
page and dwm is trying to display the title in the menu bar. Some emojis seem to
work fine while others don't. Anyway, I ended up installing and uninstalling
different fonts and X isn't exiting anymore. I tried to be systematic in my
process but at some point I gave up and I'm not sure what actually resolved the
issue. Most comments I had read suggested removing Noto Color Emoji, but when I
did the problem persisted. I tried installing the font ttf-joypixels, but again
the problem continued so I removed it. I may have done something else after that
but that's the last intentional action I remember taking. And I don't see
anything in my history that would have to do with this issue. Some emojis are
now showing up as rectangles but I'm not being booted anymore.

I guess now things are sort of fine since X isn't exiting anymore? But I still
don't know what the underlying problem was/is and that's annoying.

[forum-thread-1]: https://bbs.archlinux.org/viewtopic.php?pid=1889865#p1889865
[forum-thread-2]: https://groups.google.com/forum/#!topic/wmii/9uTQXaNBqqM
[test-1]: https://emojipedia.org/magnifying-glass-tilted-right/
[test-2]: https://www.youtube.com/watch?v=-deHlb27S9o
[test-3]: https://emojipedia.org/clapper-board/
[issue-dwm]: https://dwm.suckless.narkive.com/a0l85Le6/dev-libsl-crashes-when-redering-emojis
