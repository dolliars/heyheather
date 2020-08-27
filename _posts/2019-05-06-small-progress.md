---
layout: post
title:  "Chrome extension: Small progress"
date:   2019-05-06 13:21:42 -0400
categories: [chrome extension]
---

Hey Heather, it's me again.

I finally went over the whole Getting Started tutorial and have the basic
extension that changes the background color of a web page. Now I've started work
on the extension I've been wanting to build for the last 2 years. The extension
will add the number of minutes it'll take to read an article posted on Hacker
News next to the link.

I searched the Chrome Web store and found [a few][ext-1] [reading time][ext-2]
[estimators][ext-3] and tried them out. While they give the estimate reading
time and provide customization, you won't know the information until you're on a
page. This is the main problem I want to avoid. The idea to build this extension
came about when I had a 10 minute metro commute. I would open an article,
realize it would be too long to finish reading on the commute, and then try to
find another one. I was annoyed at this so thought about adding this feature.
Granted that now I've switched to reading a book on my commute, I still think it
would be practical.

In contrast to the other extensions which use browser action, mine will be a
[page action][google-pageAction] extension. Since it's specifically for [Hacker
News][hacker-news]. I'm pretty certain I can make it portable to other sites,
but I'm not sure how Chrome extensions work yet so we'll see. I'm thinking it'll
be possible to use on pages with aggregated lists of links. Though the first
version will only be made with Hacker News in mind.

## Where do we go from here?

Well, it's back to the [Overview page][google-overview], but this time I can
fill in the details I know about my own extension. I started by adding the
`manifest.json` file where I specify that we're using the chrome.pageAction API.
Reading the documentation I noticed that there are a few UI considerations that
I need to be aware of. For instance, since page action extensions are only
active on the pages specified, the icon can appear grayed out. Pretty sure I'll
need to provide that. I'm just going to use the icons provided in the tutorial
for now.  I can design my icons later on in the process. Next, I added some
permissions which will probably change as I build the application. I like that
there are required permissions and optional permissions. The optional
permissions can be triggered by events, which is nice if you only need the
access for a specific task.

So I haven't moved forward as quickly as I would've liked to but this is all I
have for now. I think the next step is to start working on the background
script. I feel like saying a bunch of negative things in regards to the current
status of this project but the important thing is that even though this is
moving slowly, it's moving.

[ext-1]: https://chrome.google.com/webstore/detail/reading-time/nccohhimobidpghgpnejnbkpoichbbml
[ext-2]: https://chrome.google.com/webstore/detail/pocket-article-reading-ti/lfhcmfgmiglibijdjlelmnfckmijpopg?hl=en
[ext-3]: https://chrome.google.com/webstore/detail/instant-reading-time/afipdkkndmggnmffcmepioemogfnnibf?hl=en
[google-pageAction]: https://developer.chrome.com/extensions/pageAction
[hacker-news]: https://news.ycombinator.com/
[google-overview]: https://developer.chrome.com/extensions/overview
[google-permissions]: https://developer.chrome.com/apps/permissions
