---
layout: post
title:  "Chrome extension: I persist"
date:   2019-04-29 12:41:42 -0400
eof: -arrivederci-
categories: [chrome extension, programming]
---

Hey Heather. It's me again!

Alright. I've had a wee bit of time to revisit the Chrome extension, and there's
just *so much* you can look into at each step. You could also go through it
pretty quickly but the focus here is to focus. So let's go!

Last time I went over some aspects of JSON that I didn't understand. The next
step in the [Google Extension tutorial][google-tutorial] is to add instructions
into the JSON file. By doing this, we're telling the extension which files to
reference and how to behave. Here's the example they provide:

```
{
  "name": "Getting Started Example",
  "version": "1.0",
  "description": "Build an Extension!",
  "background": {
    "scripts": ["background.js"],
    "persistent": false
  },
  "manifest_version": 2
}
```

What caught me eye here was the `"persistent": false`. What does that mean? I
have some assumptions but I don't think I should rely on that since I've never
built a Chrome extension and my assumptions are based on "I've read words
before". If we look at the [documentation regarding managing events and
background scripts][google-background], it specifies that `persistent` should be
set to `false` and that the only time it should be persistently active is when
the extension uses `chrome.webRequest` API because it's incompatible with
non-persistent background pages. I wonder when we could use that API? Let's take
a gander.

## webRequest and me being confused

This is [Google's documentation on webRequest][google-webRequest]. Those are a
lot of words. Wow! There are so many things you can do! You can fire before a
redirect is about to occur with `onBeforeRedirect`. That is very clear. The
description for the API reads:

> Use the chrome.webRequest API to observe and analyze traffic and to intercept,
> block, or modify requests in-flight.

What does in-flight even mean? As they are happening? That would make sense..
"requests as they happen". Is this tech jargon? I'm not sure I've ever heard
anyone but a pilot use that expression. And in that context it's used literally.
The sentence *seems* clear, but it's not obvious that they're talking about HTTP
requests. Oh, wait. I'm an idiot. A web request *is* an HTTP request. How did I
miss that? Derp. Moving on. 

Okay, so basically what this means is "persistent" should always be false unless
you are acting on one of the possible status of HTTP requests. I wonder what
proportion of extensions use `"persistant": true`? If it's generally set to
`false`, would it make sense to have that set as default and just require it to
be specified when `true`? At this point, I don't think Google would change it. I
think it would be considered a MAJOR change for the version. Unless it's
backwards compatible. But even then, it would just make a mess of things. I
guess that means the answers to those questions would be *moo* points.

Alright. I guess the important takeaways here are: 
1. always set `"persistent": false`, unless you use webRequest
2. webRequest API listens for HTTP request as they happen

That's what I have for now.

[google-tutorial]: https://developer.chrome.com/extensions/getstarted
[google-background]: https://developer.chrome.com/extensions/background_pages
[google-webRequest]: https://developer.chrome.com/extensions/webRequest
