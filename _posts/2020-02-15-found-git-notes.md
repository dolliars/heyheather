---
layout: post
title:  "Old notes on git"
date:   2020-02-16 00:08:17 -0086
categories: [git]
---

Hey Heather, it's me again.

I found some old notes on `git` from when I started using it in a work context
and had to look up everything, every time. I had written them in a Question &
Answer format. I think that helped me remember what was what but it's difficult
to get back to that state of mind. Anyway, I felt bad just throwing them away so
here are the notes that I took. 

I should probably add some caveat about using `--force` but I'm going to be lazy
and just say that this sentence serves that purpose.

## Questions and Answers

**How do I add all the files changed so that they are commited instead of adding
them one by one?**

`git add . `

**What are the local branches I have?**

`git branch`

**How do I created a new branch and switch to it?**

`git checkout -b bugfix/ifonlyhadwetested`

**How do I delete local + remote branch?**

Local: `git branch -d bugfix/ifonlywehadtested`

Remote: `git push origin --delete bugfix/ifonlywehadtested`

To delete both: do both.

**Dang it. There's a typo (or some other tiny mistake) and I already pushed. Or I
just want to add something to the previous commit. How do I do that?**

Make changes, and then:

`git add .`

`git commit --amend`

`git push --force`

**How do I check X number of log messages?**

`git log -3`

**How do I only see the first line of commit message?**

`git log --oneline`

**How do I remove all changes in local?**

`git checkout .`

**How do I remove untracked files?**

`git clean -f`

**How do I switch back to the branch I was just on?**

`git checkout - `
