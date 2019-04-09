---
layout: post
title:  "Chrome extensions - Versioning"
date:   2019-04-08 12:56:42 -0400
eof: -That's all folks!-
categories: [chrome extension, versioning]
---

Hey Heather, it's me again.

I have a plan to build a Chrome extension from a small project I did a few
years(!!) ago. The idea is that it'll add the amount of time it takes to read
an article next to the title or the comments on a Hacker News page. This could
be extended to other pages with article lists, and ideally the user should be
able to edit speed of reading in words/minute.

Well first of all, what even is a Chrome extension?? How do they work? Who is
its daddy, and what does he do? Well the [Google documentation][google-doc] is
pretty clear, its first section is titled "What are extensions?" and like I had
mentioned they just sound like tiny websites that [do one
thing][google-single-purpose]. This is very much like the [Unix
philosophy][wiki-unix-philo] of "building simple, short, clear, modular, and
extensible code". I'll keep this in mind as I go forward.

## Slow and steady

I'm going through this in a pretty slow manner. Mainly because I want to stop at
questions I've had and never got a chance to go through because I've felt rushed
in a *I need to know everything now!* kind of way. Hopefully it'll help me just
learn things that may seem obvious to others. So the first step in the [Getting
Started tutorial][google-get-started] is to create the `manifest.json` file.
Here's an example:

```
{
    "name": "Manifest",
    "author": "Andrew Bird",
    "version": "1.0",
    "description": "My finest work yet",
    "manifest_version": 2
}
```

Pretty straight forward. But this leads me to wonder about version numbers. We
see them all the time right? I see them when I update my system. I've never had
to number a version of an application though. The only thing that sounds close
to that are the papers I wrote in school. It kinda seems dumb, right? We had an
old version, and now we have a new version so the number goes up. But when do
you decide that the number goes up? Let's take a moment to look it up!

## Versioning

Let's start with the [Wikipedia page on Versioning][wiki-versioning]. Any time I
update my system I see something more along the lines of 3.5.1, which is a
**Sequence-based identifier**. I'm pretty sure every update I see uses [Semantic
Versioning(SemVer)][SemVer]. What does it mean? Well first of all, it applies
to applications that declare a public API. That means that it wouldn't
*generally* apply to a website. Although maybe there could be a way to harness
the power of versioning to convince people to clear their cache.. *Get our new
CSS, NOW! More JavaScript, woo!* No one wants that. Sites and applications
however often depend on libraries, or components, or packages, or plugins,
*ohmy!* So if you're using the public API of any of these, that tells you "this
is how to use me!" and they change the way you're supposed to use it, *you're
gonna have a bad time*. Hence the use of versioning as means to communicate the
type of update that was done. SemVer suggests "a simple set of rules and
requirements that dictate how version numbers are assigned and incremented" and
it goes like this MAJOR.MINOR.PATCH. Baffled? Well it just means that if your
update is incompatible with the public API that was declared, then you increment
the MAJOR number. If it's an update to a functionality and is
backwards-compatible then you increment the MINOR, and if it's a
backwards-compatible bug fixes, PATCH.  The [F.A.Q.][SemVer-faq] on SemVer's
page is a pretty great resource and I invite you to take a gander if you've ever
wondered about versioning. It answered my question about why some would start
with `0` as in `0.1.2`. Answer: It's used in the initial development stage.

Another important thing related to versioning not mentioned on the SemVer page
is the almighty ChANgELoG. Which is named explicitly for what it is but no one
can decide how to type it. It's a summary that should be understandable to a
person. You can see the [keep a changelog site][changelog] for details. If you
change your API, here is where you would tell everyone how it changed. The
combination of these processes makes for a clearer history. You can be oblivious
to a lot of this when you use a package manager. Not that you wouldn't use one
but I mean there's a pretty big difference in a package going from `2.8.0` to
either `3.0.0` or `2.9.0`. You're kind of missing out on important communication
when you don't know what these numbers signify and how they work within the
general environment. It also looks like information that everyone just kind of
knows, so it's easy to see how someone can just go along with it and increase
numbers without understanding what it's supposed to communicate. 

## Wait this was about the Chrome Extension

Indeed it was! SO! Coming back to the Chrome Extension. What does it mean for us
here? Google has [documentation][google-version] that specifies a few rule and
mentions that they have an autoupdate in place. The first version of the Chrome
extension that will be published will be `version 1.0`. If I make any updates
then I'll adjust accordingly. If I had been developing the extension in a
collaborative manner then I could've started with `0.1.0`. I can still use this
to plan each step I'm going through. The first being just getting through the
tutorial. And anything to do with what I specifically want to build will start
at `0.2.0`. We'll see how progress goes.

## In conclusion

Wow. I didn't know I'd talk so much about versioning and spend a whole day
thinking about it. I thought I'd just mention it and then go on about
`chrome.webRequest API`. I had a note about synchronous and asynchronous calls
so I thought maybe I'd get to that. To be honest though the specific note is
"Oooo synchronous and asynchronous calls! Exciting stuff!" I mean it is but that
note doesn't mean anything. Oh well! That'll be for another time then! byyeee

[google-doc]: https://developer.chrome.com/extensions
[google-single-purpose]: https://developer.chrome.com/extensions/single_purpose
[wiki-unix-philo]: https://en.wikipedia.org/wiki/Unix_philosophy
[google-get-started]: https://developer.chrome.com/extensions/getstarted
[wiki-versioning]: https://en.wikipedia.org/wiki/Software_versioning
[SemVer]: https://semver.org/
[SemVer-faq]: https://semver.org/#faq
[changelog]: https://keepachangelog.com/en/1.0.0/
[google-version]: https://developer.chrome.com/extensions/manifest/version

