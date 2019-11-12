---
layout: post
title:  "Don't publish secrets"
date:   2019-11-12 04:06:42 -0400
categories: [ git, protip]
---

Hey Heather, it's me. Again.

ProTip: don't publish your access tokens to a public repository. I hear it's bad
practice. It's a pretty simple mistake to make when you're working on a personal
project. I just thought *let me just put this on github doopti dooo...  ohno*.
Thankfully services that provide access tokens can easily regenerate a new one.
After publishing the repo, I immediately switched it to private and though the
chances of some malicious human or bot acquiring it seemed slim, it's best not
to take such risks lest it cost a few doubloons. However, instead of generating
a new access token, I wanted to see if there was [a way to change it with
git][git-rewrite-history] by re-writing the history. I can't pass up an
opportunity to potentially use interactive rebase. *Who could resist that!*
However, at this time of day, in this part of the country, localized entirely
within my living room I can barely make sense of what I am reading. My quick
search did yield a fruitful piece of knowledge. There's a command `git
filter-branch` that let's you remove a file in your entire history.

Basically, this post's objective was to document that 1) `git` is great, and 2)
`git` has a way to remove a file from every commit with `git filter-branch`.
Because who hasn't committed allPasswords.txt to a project they want make open
source. Anyway, I still need to try it out to see how it works.

I did end up regenerating a new access token which I added to a configuration
file. And that file was added to .gitignore. I'd still like to know if there's a
straightforward way to edit a single line in one file and have that line
re-written in the entire history. I'll leave that for another day.

[git-rewrite-history]: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
