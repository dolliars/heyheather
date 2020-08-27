---
layout: post
title:  "Building a shell - A digression of sorts"
date:   2019-04-06 17:03:42 -0400
categories: shell
---

Hey Heather! It's me again.

I know. This post isn't about the Chrome extension. I'm going to write about
that too so there should be another post soon. For now, let me tell you about
this workshop I attended.

Yesterday, I learned a bit about building my own shell. The idea of the workshop
is to get you to understand how Unix processes work. There was mention about
clarifying some of the things that are misunderstood about POSIX shells but I
don't know what that means yet. It's pretty cool that we'll end up with a
working shell. I got `$$` to print out and take in an input and it sparked joy.
This is good. A feeling. Here's the link to Julian's [Build your own shell
repo][gh-build-shell] if you're ever interested in making your own.

The reason to go through this is best summarized by the creator's words: 
> The shell is at the heart of Unix. It's the glue that makes all the little
> Unix tools work together so well. Understanding it sheds light on many of
> Unix's important ideas, and writing our own is the best path to that
> understanding.

Sounds great, right?! After the workshop I took a bit of a step back and
[went][wiki-unix] [over][wiki-unix-philo] [a bunch][wiki-unix-fs] [of
Wikipedia][wiki-shell] [articles][wiki-dennis] [again][wiki-ken] because of
course I did. I'm trying to get into the habit of closing my tabs in general. It
is difficult. But reading the Unix-related wikis makes programming seem so
simple and logical. Of course things should be modular! Of course they should do
one thing well! Isn't this how everyone thinks? Of course you think of other
developers who will work with your code in the future. But maybe we sometimes
forget and then complacency sets in. I'll try to veer away from that. I can and
should always try to do better. Okay so let's close these tabs now.

## So the workshop

In the workshop I started out writing [stage 1][gh-stage1] in C but that was a
mistake. This is because in the second step, we need to split the line that was
input. Although C doesn't have .split(). It does have `*strtok`, which would
break a string into a series of tokens using a delimiter and would return a
pointer to the first token found. And this is when I remembered that I actually
don't know C because I haven't used pointers. Beyond knowing that it's a
variable that stores the address in memory of another variable, I don't know
what I'd do with it. I've read that it's used to dynamically allocate memory,
but since I haven't done it yet it's still very abstract. Even if I did
understand pointers though, there were other considerations that I wasn't aware
of and now can't quite remember. It has something to do with the way C would
handle the string I think. But I stopped around there. Considering that Julian
said "let's say you don't know Python at all, you should still do it in Python".
I think it's best to listen. It'll be less of a pain and I'll still learn. And
of course he offered support in the future if I want to go back and try to do it
in C. But the point now was to get something started. Here is what I wrote in C:

```
char *line = NULL;
size_t len = 0;
ssize_t nread;

for(;;) {
	printf("$$ ");
	fflush(stdout);
	
	nread = getline(&line, &len, stdin); 
	
	printf("%s", line);
	if ( nread < 0) exit(0);
}
```

It's pretty straightforward: show the prompt, get rid of anything that was input
previously, read the line, print it, exit if `nread` returns less than 0. Do
this forever. I'm not sure I understand what `nread` is doing. Let's look at
that for a second. 

Initially we set `nread` to be of type `ssize_t`. This type is used to
represent the size of an allocated block of memory. That variable then takes the
output of `getline`. Looking at the man page for `getline` it says that it
"reads an entire line from stream and stores the address of the buffer
containing the text into the line pointer". So basically we're just filling what
was "empty", which here was `line` and `len`, with the standard input and it's
returning the number of characters read. If it fails it'll return -1 and this is
why we needed to set the type of nread to `ssize_t` because it needs to be
signed typed, which means it can represent -1.

It's amazing to me how much information is packed into just a few lines of code.
Wow! Well that's about how much I could do in C before I was encouraged to try
building a shell in Python. All I've got in Python is:

```
while True:
	print("$$")
	line = sys.stdin.readline()
	args = line.split()
	print(args)
```

As you can see there is work to be done. For the first stage of the workshop,
it's just to get something basic working. Here is what the simplest shell should
look like:

```
loop
	print "$ "; flush(stdout)
	line = getline(stdin).split()
	if eof(stdin): exit(0)
	pid = fork()
	
	if pid == 0:
		execvp(line)
	waitpid(pid)
```

I think it's pretty neat. You'll probably see more posts regarding this project.
And now, to work on a Chrome extension!


[gh-build-shell]: https://github.com/tokenrove/build-your-own-shell
[wiki-unix]: https://en.wikipedia.org/wiki/Unix
[wiki-unix-philo]: https://en.wikipedia.org/wiki/Unix_philosophy
[wiki-unix-fs]: https://en.wikipedia.org/wiki/Unix_filesystem
[wiki-shell]: https://en.wikipedia.org/wiki/Shell_(computing)
[wiki-dennis]: https://en.wikipedia.org/wiki/Dennis_Ritchie
[wiki-ken]: https://en.wikipedia.org/wiki/Ken_Thompson
[gh-stage1]: https://github.com/tokenrove/build-your-own-shell/blob/master/stage_1.md
