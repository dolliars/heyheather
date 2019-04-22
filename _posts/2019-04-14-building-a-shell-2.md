---
layout: post
title:  "Building a shell - fork() in the road"
date:   2019-04-14 23:14:42 -0400
eof: -So it goes-
categories: [shell, fork]
---

Hey Heather! IT'S me again.

I went to the second workshop for building my own shell. I'm really enjoying
being confused haha! I've been over the "Executing a command" section in the
instructions of [stage 1][gh-stage-1] and I think I only partially understand
what is happening. It's a key part so I think it's important to go over it.
Here's the mock code relating to executing provided in the instructions:

```
pid = fork()
if pid == 0:
    execvp(line)
waitpid(pid)
```

I'm doing it in Python so the links to the system calls will be to its
documentation. So the first thing we do is [`fork()`][python-doc-fork] which
forks a child process and does two things: returns 0 to the child and returns
the child's process id to the parent. At this point, we have "two parallel
universes", parent and child (I'm not sure what that means yet). After that we
[`execvp()`][python-doc-execvp]. This system call executes a new program by
replacing the current process. Then we have another eponymously named system
call [`waitpid()`][python-doc-waitpid] that waits for the child process to
finish running.

## I think I get it now! 

As I was writing this post I was still trying to wrap my head around what this
all meant. Thankfully, there's a resource list in the [Build your own shell
repo][gh-build-shell]. Going over [another workshop's repo][gh-kamal-shell]
(written by Kamal!), I found what I was looking for in section 4. The question I
should've asked was *why fork() at all?* I mean we could just execute the
command, couldn't we? Indeed! We could. But the way `execvp()` works is that it
**changes** the current process. Kamal sums it up super clearly:

>The `exec` call transforms the current process into the command we specify. So
>our shell's process is replaced by `ls` or whatever we chose to run. Once that
>program is done, the process exits—no more shell.

I did *not* catch that at first! I was following along but didn't see the
importance of `fork()`. It's necessary because of the way `execvp()` works. If
we didn't use `fork()`, our shell would metamorphose into the command we give it
and then die! *What is wrong with it!* Instead of watching our lonely shell
[seppuku][wiki-seppuku] itself, we let it fork, and of course this creates a
child which gives our shell meaning of life as it awaits the child's return. I
know, right? Since the new process created by `fork()` is initially a copy of
itself, I think of it more as a clone. If you want a better illustration of
`fork()` in this initial state, you can check out [this YouTube
video][YT-fork-arnold] that sums up what fork is to itself in a short but clear
manner. Don't associate it too much with clone though because there's also
`clone()` which is different than `fork()` but I won't get into that now.

All this is pretty cool. I have some more work to do in stage 1 but I'm also
going to start to look at stage 2 which is files and pipes. I'll keep you
posted!

[gh-stage-1]: https://github.com/tokenrove/build-your-own-shell/blob/master/stage_1.md
[python-doc-fork]: https://docs.python.org/3/library/os.html#os.fork
[python-doc-execvp]: https://docs.python.org/3/library/os.html#os.execvp
[python-doc-waitpid]: https://docs.python.org/3/library/os.html#os.waitpid
[gh-build-shell]: https://github.com/tokenrove/build-your-own-shell
[gh-kamal-shell]: https://github.com/kamalmarhubi/shell-workshop
[wiki-seppuku]: https://en.wikipedia.org/wiki/Seppuku
[YT-fork-arnold]: https://www.youtube.com/watch?v=Ra-wC05lZi4
