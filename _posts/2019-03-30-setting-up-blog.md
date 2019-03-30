---
layout: post
title:  "Setting up a blog with Julia's instructions!"
date:   2019-03-30 11:49:42 -0400
eof: -30-
categories: jekyll update
---
Hey Heather, it's me!

I finally set up this blog! Yay! I read through Julia's post [How to set up a
blog in 5 minutes][julia-blog-post] (which was a total lie by the way, it took
wayy more than 5 minutes). I was confident at the start because I read through
it and though "oh hey I know some of these things!" and then I had to set up a
Ruby environment. I don't even know what happened. I've done it before but it
was still super confusing.

This is how it went: What's a Ruby environment? What is Octopress? Aaaaand now I
have 31 tabs open.

I just closed all the tabs and went back to Julia's post before things got
overwhelming. I really like reading her blog because it's as if she's actually
saying the things to me. I probably hang out with her in my head more than I do
in real life haha! 

Anyway, so the most useful information I found was going through the Jekyll site
[Quickstart][jekyll-quick-start], [Installation][jekyll-ruby-installation], and
the [arch wiki page on Ruby][archwiki-ruby]. The blog post had some information
that was out of date, notably running `rbenv rehash`. It's now deprecated
because the behaviour is now included in rbenv core.

Another helpful resource was [this article][linux-path] that just goes over
some basics about what the $PATH is in Linux. There is so much I don't know
still!

Even though I set up this blog, I'm still confused about how some parts work.
Getting set up is **hard**. For some reason I thought it'd be easier. Then I
found [this tutorial][dev-environments] that says: 
> Unfortunately, setting up a fully functional native development environment
> can be a challenging and frustrating process.

Reading that is super reassuring. This is a hard thing. And it's okay that it
takes time to understand. Yay for learning hard things! And this begs the
question: 

**What have I learned here?**

What is a Ruby Gem? Well, it can be confusing because there is RubyGems, which
is a package manager for distributing Ruby programs and libraries. And then
there are Gems which are packages that contain the information of the files to
install. I'm spewing this out but I think I'm still confused, mostly about how
it works. But that's okay, I'll probably have to go over this in the future.

What does it mean to set up a Ruby environment? It just means setting up a way
to tell your application "Use this version of Ruby".

What is octopress? It's a Ruby Gem for writing a deploying Jekyll blogs.

I also learned that some information on blogs may no longer be relevant, so
always check the documentation.

Also: look for documentation specific to your OS! I keep forgetting to do this!

[julia-blog-post]: http://jvns.ca/blog/2014/10/08/how-to-set-up-a-blog-in-5-minutes/
[jekyll-quick-start]: https://jekyllrb.com/docs/
[jekyll-ruby-installation]: https://jekyllrb.com/docs/installation/
[archwiki-ruby]: https://wiki.archlinux.org/index.php/ruby
[linux-path]: https://opensource.com/article/17/6/set-path-linux
[dev-environments]: https://www.learnenough.com/dev-environment-tutorial
