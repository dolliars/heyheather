---
layout: post
title:  "Building a shell: pipe down!"
date:   2019-04-23 02:01:42 -0400
categories: [shell, pipes]
---

Hey HEATHER! It's me again.

Unfortunately I didn't get to accomplish as much as I would've liked to last
week. It doesn't help that my sleep schedule has been messed up for some time.
Woe is me. Anyway. On Friday, I went to the shell workshop and started [Stage
2][gh-stage-2] which is on Files and Pipes.

I went over the notes, the man pages, the code, I asked some questions. But when
I got home, I realized that I seldom use pipes! Besides `dmesg | tail`,
`journalctl | tail`, and the thankfully rare plumbing problems, I can't think of
another instance where I would pull out a pipe. Which just means I don't know
the _true power_ of pipes. Let's see if I can change that and conjure up some
powerful pipes.

## Pages, man.
Let's read man pages again. In the [Linux Programmer's manual][man-pipe-linux],
the definition reads "pipe() creates a pipe", so far so good. The said pipe is
"a unidirectional data channel that can be used for interprocess communication".
Simple enough. Hmm, interesting. The tutorial has a link to the [FreeBSD
manual][man-pipe-fbsd] as well, so I checked it out. It says "the pipe()
function creates a pipe, which is an object allowing bidirectional data flow
(...)". Ohno.

Now that I've emerged from the rabbit hole (*thanks pomodoro timer!*), I
acquiesce that although it's possible to use pipes in a bidirectional manner on
some systems (not Linux tho), it's best to use them in the conventional way. I
would've like to know in which circumstances pipes could be used bidirectionally
but I think this [Stackoverflow answer][SO-pipe-syscall] is enough to quell my
curiosity. It just states that the [POSIX standard for pipes][man-pipe-posix]
doesn't specify their directional behavior. Moving on.

## Wrong model
When I started looking into pipes, I thought I had a good idea about how they
worked. It turns out I was wrong. To illustrate, this is the model of how I
thought of pipes:

```
dmesg     |  less
↳read end    ↳write end
```

But it didn't make sense when I thought about it. When you ask the question
"what about when there's more than one pipe?" For instance:

```
dmesg     | grep 'usb' |  less
↳read end   ↳read end     ↳write end
```

You can't just read something and pass it on without writing. And here is where
I finally understood this part of the definition:
>The array pipefd is used to return **two file descriptors[fd]** referring to
>the ends of the pipe. pipefd[0] refers to the read end of the pipe. pipefd[1]
>refers to the write end of the pipe. 

I was aware that the **output** of one became the **input** of the other command
but clearly I didn't grasp what that meant. That is until I saw the first two
figures on [this website][notes-pipes]. The gist of it is that pipes transfer
data from a `write` endpoint to a `read` endpoint. Here's the command again.

```
dmesg | grep 'usb' | less

// flow
write fd -> stdout -> stdin -> read fd -> write fd -> stdout -> stdin -> read fd
```

The flow of the data is from left to right and goes something like this:

1. We make a system call to `dmesg` that writes to the stdout end of the pipe;
2. the data flows to the stdin end of said pipe into the read fd of `grep`;
3. `grep` writes to the stdout end of the second pipe;
4. the data again flows to the stdin end of the pipe;
5. where it is then read by less.

Woah. I mean, I'm literally repeating what I've read, but it just seems to make
so much more sense now. Like a well constructed aqueduct each end ties into the
other. I don't need to conjure anything up. Pipes are powerful in themselves.

This turned out to be a great bedtime story somehow. Which reminds me where I
ought to be at this time. Dang it.

Last note: I really like the YouTube channel Computerphile and it turns out they
have [a video on Unix pipeline][YT-computerphile-pipes] presented by [Brian
Kernighan][wiki-brian]. I like how he explains the benefits. Enjoy!

[gh-stage-2]: https://github.com/tokenrove/build-your-own-shell/blob/master/stage_2.md
[man-pipe-linux]: http://man7.org/linux/man-pages/man2/pipe.2.html
[man-pipe-fbsd]: https://www.freebsd.org/cgi/man.cgi?query=pipe&sektion=2&manpath=FreeBSD+11.1-RELEASE+and+Ports
[SO-pipe-syscall]: https://stackoverflow.com/questions/5385534/posix-pipe-syscall-in-freebsd-vs-linux
[man-pipe-posix]: http://pubs.opengroup.org/onlinepubs/9699919799/functions/pipe.html
[notes-pipes]: http://web.cse.ohio-state.edu/~mamrak.1/CIS762/pipes_lab_notes.html
[YT-computerphile-pipes]: https://www.youtube.com/watch?v=bKzonnwoR2I
[wiki-brian]: https://en.wikipedia.org/wiki/Brian_Kernighan
