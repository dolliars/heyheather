---
layout: post
title:  "Connect phone"
date:   2023-06-14 13:08:17 -0400
categories: [phone]
---

Why is it _sooo_ hard connect my phone to a computer to transfer files?! It's
infuriating. Hmm? I wonder if infuriating is the right word.

Definition:

> making one extremely angry and impatient; **very annoying**.

Yupp!

I'm all for offering the option as a service. But it seems like every company is
just obfuscating things we can _do_ with technology. You know, like move a file.
Everything is cloud this. Cloud that. CloudCloudCloud. They chose the right word
for it though.

Definition:

> 1. a visible mass of condensed water vapor floating in the atmosphere,
typically high above the ground.
> 2. **a state or cause of gloom, suspicion, trouble, or worry.**

Yeah, that sounds about right.

Maybe I'm exaggerating a bit. But every time I need to connect my phone, it's
such a hassle. So this post is me talking to my future self for when I
inevitably have to do it again.

## Steps

1. **Make sure you're using the correct cable**. Some cables are only used for
   charging and won't work for data transferring. You will think that they're
   the same. They are not. Fortunately, there's only 2 cables so you have a
   50/50 chance of getting it right
2. **Access Developer Mode on your phone**. You switched it off. To access it
   again, go to `Settings > About phone > Software information` and quickly tap
   on Build number seven times
3. **Enable transferring files** by going to Settings > Developer options >
   Default USB configuration (under Networking) > Transferring files
4. **Run `# jmtpfs /mnt/phone/`**
   <br>If you get the message: **No mtp devices found.**
   <br>Double check you are using the correct cable, then run the command again. You
   should get something like `Device 0 (VID=04e8 and PID=1234) is a Phone model (MTP).`
5. **To disconnect** run `jmtpfs -u /mnt/phone/`
   <br>Oh. Has that randomly started and continued to give you an error message
   because of $reason??
   <br>Then try `fusermount -u /path/to/where/you/connected/`
   
Other useful commands that may or may not be relevant:

```
$ lsblk
$ mount /dev/sdc1 /mnt/xdisk
$ ls /mnt/xdisk/
```

## resources consulted:
- [Ask Ubuntu][askubuntu-mtp-device]: My MTP capable device is not detected?
- [Arch wiki][wiki-arch-transfer-protocol]: Media Transfer Protocol

gl;hf

[askubuntu-mtp-device]: https://askubuntu.com/questions/417323/my-mtp-capable-device-is-not-detected-what-can-i-do-about-that
[wiki-arch-transfer-protocol]: https://wiki.archlinux.org/title/Media_Transfer_Protocol
