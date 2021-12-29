---
layout: post
title:  "Anchors: a way to phish"
date:   2021-12-29 16:08:17 -0500
categories: [links, security]
---

Hey Heather, it's me again.

_\* I'm going through some old drafts that have been laying around and polluting
my directory. I'll be reviewing and posting some of them._

**tl;dr**: there was a [vulnerability][blog-vulnerability] with using
`target="_blank"` where a linked page could access _some_ information of the
origin page and use it, for instance by redirecting the page and phising for
credentials. [Most browsers][mdn-anchor-target] now implicitly set
`rel="noopener"` on `<a>` elements which have `target="_blank"` set so it's
basically a non-issue now.

A while ago I wrote a note to myself to "look into `noopener` and `noreferrer`".
You're likely to see one or both of these in markup such as this:

```
<a href="#someLink" target="_blank" rel="noopener noreferrer">Link text!</a>
```

I didn't know what these meant so looked it up and found some sites recommending
always using them whenever `target` was set to `_blank`. I've definitely used
`target="_blank"` before but can't say I recall ever setting those attributes.
Let's look into it.

There are two parts to this: the `rel` attribute, and the `target` attribute.
First off, `rel` is used to state the relationship between the link itself and
the current document. For instance, you see it in html `<head>` with the
stylesheet, like so `<link rel="stylesheet" type="text/css" href="/assets/css/main.css">`.

`rel` doesn't have a default value so if omitted on `<link>` or `<form>`, the
link won't be created. If you have a website with a stylesheet, you can test
this out by removing the `rel="stylesheet"`. You can even try it here by using
the inspector and editing the markup. All the styles disappear. It works
differently on the `<a>` and `<area>` elements. They'll still create the link
even if `rel` isn't set.

Now, the `target` attribute is used to tell the browser where to display
the link. The default value for it is `_self` which means the current browsing
context. Another value you'll see is `_blank` which opens the link in a new tab,
or in a new window if configured so by the user. This is the type of thing you
don't think about too much. You're just opening a link here, there, everything
seems fine. But the thing about using `_blank` is that — and this is before
browsers update the behavior — when it opens a new tab, it also passes along the
reference to the [window that opened the link][mdn-window-opener] which meant
that "if window A opens window B, B.opener returns A". The problem with this is
that you can do stuff with that reference. Stuff like redirects. As the MDN
article states this "makes phishing attacks possible, where a trusted page that
is opened in the original window is replaced by a phishing page by the newly
opened page".

This browser behavior is why you'll see the recommendation to add the
`rel="noopener noreferrer"` anytime you have `target="_blank"`. But you no
longer have to worry about this if you're using a [modern
browser][caniuse-implicit]. But *still*!! If I'm checking the dates correctly,
this was only resolved in the last couple of years. This was still a problem
when I initially started to write this post! I keep being impressed by the
amount of work there is to do in this field.

Oh, and another thing I learned when I read the documentation for
[noreferrer][mdn-noreferrer]: writing `rel="noopener noreferrer"` is redundant
since `noreferrer` will make "the referrer unknown (...), and creates a
top-level browsing context as if noopener were also set". In other words,
`noreferrer` implies `noopener`.

Things change so be sure to check the docs!

[blog-vulnerability]: https://www.jitbit.com/alexblog/256-targetblank---the-most-underestimated-vulnerability-ever/
[mdn-anchor-target]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-target
[mdn-window-opener]: https://developer.mozilla.org/en-US/docs/Web/API/Window/opener
[caniuse-implicit]: https://caniuse.com/mdn-html_elements_a_implicit_noopener
[mdn-noreferrer]: https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/noreferrer
