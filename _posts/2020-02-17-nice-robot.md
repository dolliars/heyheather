---
layout: post
title:  "A nice robot"
date:   2020-02-17 23:08:17 -0500
categories: [misc, bot]
---

Back in August, I wrote a [twitter bot][twitter-bot]. What this robot does is it
asks the question "What did you do today that was kind for someone else?" once
per day. The context of this is that I was listening to [episode 22][fs-E22] of
the podcast The Knowledge Project. In the episode, the host Shane Parrish is
discussing with Adam Grant and says that he asks his children this question. I
thought it was nice and wondered what I'd answer on any given day. And that's
where I got the idea for it.

## What I learned

To implement this I used: the Twitter API, an AWS EC2 instance, JS, and the
Twitter API client [twit][npm-twit]. As I was looking around for explanations
and guidance, I found [this resource][shiffman-twitterbot] created by Daniel
Shiffman which contains explanations and tutorial videos for creating a bot.
Since this was a few months ago, I've forgotten some of the elements I struggled
with. One thing I do remember though is a problem I encountered when trying to
use the Twitter API.

From the beginning, my plan was to tweet the same message once per day. However
if you check the [documentation for POST statues and updates][twitter-api-post],
it specifies that:

> For each update attempt, the update text is compared with the authenticating
> user's recent Tweets. Any attempt that would result in duplication will be
> blocked, resulting in a 403 error. **A user cannot submit the same status twice
> in a row**.

Ohno. My plan! Foiled by what is undoubtedly meant to prevent spam. In order to
circumvent this problem, I thought I could add some sort of counter. Adding the
[ISO-8601 date][wiki-iso8601] would be repetitive I thought since tweets already
have a date. And having a counter start at 1 in August also felt incorrect. So I
decided to add the day number (also known as the [ordinal
date][wiki-ordinal-date]) excluding the year. This means that January 1st is Day
1, February 1st is Day 32, and so on and so forth. It worked well. The bot is
out there in the world waiting for tomorrow to quietly tweet away its question
to anyone who will happen to come across it.

Soon however, it'll be silenced. My main objective for the project was to force
me to finally finish a project, to finish *something*. I got to see how AWS EC2
worked and how to use Twitter's API. But the free tier on the EC2 instance is
almost up I believe so I'll be taking it down. Its been up for about 182 days
now, so that's something. Half a year ain't bad.

[twitter-bot]: https://twitter.com/BekindBot
[fs-E22]: https://fs.blog/adam-grant/
[npm-twit]: https://www.npmjs.com/package/twit
[shiffman-twitterbot]: https://shiffman.net/a2z/twitter-bots/
[twitter-api-post]: https://developer.twitter.com/en/docs/tweets/post-and-engage/api-reference/post-statuses-update
[wiki-iso8601]: https://en.wikipedia.org/wiki/ISO_8601
[wiki-ordinal-date]: https://en.wikipedia.org/wiki/Ordinal_date
