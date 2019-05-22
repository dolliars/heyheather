---
layout: post
title:  "Building a shell: recap and dup2()"
date:   2019-05-22 02:35:42 -0400
eof: -Such is life-
categories: [shell, pipes, dup2() ]
---

Hey Heather, it's me again.

As you're probably aware, I'm still working on building a shell. Since I last
wrote about the workshop, we've had a two week break and two meetings. I've had
trouble understanding how [dup2][man-dup2] works so I haven't really moved past
pipes. I'm glad I've been writing about the process though. The blog has served
as notes that I reference now and again. Recently I tried to explained what I've
learned so far and had some trouble expressing it. I'm glad I practiced
verbalizing it though. So let's recap.

## Basics

First of all, [*what's a shell ?*][wiki-shell] It's the user interface used to
access the services of an operating system. Your OS provides a bunch of services
to manage files, processes, monitoring, configuration, and the shell is used to
access them. You can think of a simple example just to have an idea on what's
going on. For instance, if you want to delete a file your shell is accessing the
"delete" service offered by your OS. Using a command line interface (CLI) you
could access the service by writing `rm file`. On a graphical user interface
(GUI) you could access the service by right-clicking on the file and selecting
`Delete`.

The way it works is by taking user input and running the commands. When
implementing a shell, we know that it needs to do this continually. Therefore it
needs to be an infinite loop. I'm currently reading The Dream Machine by
Mitchell Waldrop and I just read a passage that reminded me of the shell. It's
actually referencing [John von Neumann's][wiki-neumann] description of how the
central control unit is supposed to execute programs: 

> He envisioned the central controller as going through an endless cycle: fetch
> the next chunk of instructions or data from the memory unit, execute the
> appropriate operation, and then send the results back for storage in memory.
> Fetch, execute, return.

I guess it's similar to most feedback loops. What else do we have? Well, there's
[`fork()`][man-fork] and [`execve()`][man-exec] that need to be used together.
First, we `fork()` to create a copy of the current process. Now we have a parent
and a child. In the child process, we execute the command with `execve()`.
Thus, the child process becomes the command that is executed and the parent
waits for that process to finish with [`wait(2)`][man-wait].

To implement piping, we need to add [`pipe2()`][man-pipe] and `dup2()`. What we
need to do when piping is to attach the write end of one process to the read end
of another. We achieve this by manipulating the file descriptors. This is where
I get confused. I'll try to explain. 

## An attempt is made

Every process we run has the same first file descriptors: 0 for standard input,
1 for standard output and 2 for standard error. If we run `ls` we see the output
on our screen. When we run `ls | less`, we want the output of `ls` to become the
input of `less`. So the standard out [1] of the first command needs to become
the standard in [0] of the second command. With `pipe2()` we create a data
channel that has a read end fds[0] and a write end fds[1]. So for instance, when
we have `ls | less` we create one pipe which returns two new file descriptors.
Let's say 3 and 4 in this example. In this case we'll have:

- pipefd[0] is 3 which is the read end
- pipefd[1] is 4 which is the write end

Now we'll want: 
- the stdout of `ls` (which is 1) to become 4 (write end of the pipe), and
- the stdin of `less` (which is 0) to become 3 (read end of the pipe)

Here is where we use `dup2(oldfd, newfd)`. This system call will create a copy —
you can also think of it as an alias — of the file descriptor and change it from
the oldfd to the newfd. So for `ls` we'll have `dup2(4, 1)`. And for `less`
`dup2(3,0)`. I've written out the different parts below and it kind of helps me
untangle the different parts.

```
        ls   |   less
stdin    0        0
stdout   1        1
stderr   2        2
        ...      ...
 _______________
| 3   pipe    4 |
 ---------------

#dup2(int oldfd, int newfd)

         dup2
ls:   4 write, 1 out
less: 3 read,  0 in

```
I've spent a lot of time looking at this and still don't think I get it. I'm not
sure which part though. I'll take a step back for now. Some distance may help.
Here's the current program for the shell. There's still a lot missing but you
can read the pipeline function and see how `dup2()` is used. If I didn't explain
well enough, maybe reading the code will help.

```
def exec_redirected(args, fds):
    pid = os.fork()
    if pid == 0:
        for (childfd, parentfd) in fds.items():
            os.dup2(parentfd, childfd)
        os.execvp(args[0], args)
    return pid

def exec_pipeline(line):
    commands = line.split('|')
    fds = {0:0, 1:1, 2:2} # mapping

    for command in commands[:-1]:
        (r, w) = os.pipe()
        fds[1] = w
        exec_redirected(command.split(), fds)
        os.close(w)
        if fds[0] != 0:
            os.close(fds[0])
        fds[0] = r

    fds[1] = 1
    pid = exec_redirected(commands[-1].split(), fds)
    if fds[0] != 0:
        os.close(fds[0])
    return os.waitpid(pid,0)
```

## Digressing is okay

A few weeks back, while at the workshop, I mentioned to the headmaster that I
had spent some time trying to understand why the Linux manual mentioned that
pipes were unidirectional and the FreeBSD manual said bidirectional. I phrased
it in a way that said "oh I justed wasted time on this useless information". I
was quickly corrected and told something along the lines of: 

> Don't say that. You never know when this type of information will be useful
> and help you find the source of a mysterious bug.

I was happy to hear it. What I believe I was trying to express was
disappointment in the fact that I hadn't moved past pipes. Did I actually think
it was useless information? Not exactly. I guess what I meant was that it didn't
get me closer to building the shell. But I did learn something new and got to
share it with others.

[man-dup2]: http://man7.org/linux/man-pages/man2/dup2.2.html
[wiki-shell]: https://en.wikipedia.org/wiki/Shell_(computing)
[wiki-neumann]: https://en.wikipedia.org/wiki/John_von_Neumann
[man-fork]: http://man7.org/linux/man-pages/man2/fork.2.html
[man-exec]: http://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html
[man-wait]: http://pubs.opengroup.org/onlinepubs/9699919799/functions/wait.html
[man-pipe]: http://man7.org/linux/man-pages/man2/pipe.2.html
