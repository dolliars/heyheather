---
layout: post
title:  "Why is my wifi down? An occasional problem"
date:   2019-12-12 12:45:42 -0400
categories: [ misc, wifi, arch]
---

I accidentally turned off my computer when moving it around and this broke wifi.
I brought this upon myself really. A few days ago I did a system update and
didn't reboot. Honestly, I just have a heedless heuristic when it comes to
rebooting which goes something like this: reboot when kernel is updated or
whenever I accidentally closed all tabs in the browser. I could do better.
Anyway! I find this to be the most annoying problem on a laptop because you're
relegated to using your phone for search. This isn't the first time I've had
issues with wifi. It had been a while though so I didn't remember what I had
done. This will serve as a reminder for when it will inevitably happen again.
FYI: the distro I use is Arch Linux.

## Previous problem

Because it's the most frequent case that has happened to me, it's the first one
I should check whenever wifi isn't working. On my laptop, the F8 key toggles the
wireless card. That key is right above the number 7 so I've inadvertently
pressed it without noticing. I've also seen laptops with an inconspicuous switch
that will also turn off the wireless card. The fact that these slips are quite
subtle makes it harder to figure out what you did and just emphasizes the _I
don't even know what happened!_ If you want to check if you've toggled the
wireless card you can use `rfkill`. You can read the documentation on the [arch
wiki][arch-wireless-rfkill].

```
$ rfkill list
---------------------
2: phy0: Wireless LAN
	Soft blocked: no
	Hard blocked: no
```

If **Hard blocked** is set to yes, you'll need to toggle the hardware switch. If
**Soft blocked** is set to yes then you can use the command `# rfkill unblock
wifi`.

## What happened this time

I'm not sure anymore, I was supposed to write this two weeks ago. But I do know
my initial reaction to wifi not working was _But I didn't even do anything!_ Once
I got over that I started trying to debug the problem. I remember it was pretty
straightforward to figure out what the issue was but not how to resolve it.
It's a little difficult to remember what I did exactly because now that
everything is working I'm getting no error messages. Anyway I'll go from memory
and write the commands I _believe_ I used.

First command I ran was probably `netctl stop home`, followed by `netctl start
home`. I believe this would have brought up a message saying that it didn't work
and that I should check `journalctl -xe` and `systemctl status
netctl@home.service`. An error message said something along the lines of
**firmware missing**. I ran two other commands `ip addr` and `lspci -v`. The
first command didn't show my network device but it existed when I ran the second
command. Here's what the output of these commands may look like if working
correctly:

```
$ ip addr
  1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      inet 127.0.0.1/8 scope host lo
         valid_lft forever preferred_lft forever
  2: enp0s31f6: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
      link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff
  3: wlp58s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
      link/ether 70:5a:b6:8a:a0:87 brd ff:ff:ff:ff:ff:ff

$ lspci -v
  (... this output has been shortened ... )
  3a:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
	  Subsystem: Intel Corporation Dual Band Wireless-AC 8265
	  Flags: bus master, fast devsel, latency 0, IRQ 126
	  Memory at ec000000 (64-bit, non-prefetchable) [size=8K]
	  Capabilities: <access denied>
	  Kernel driver in use: iwlwifi
	  Kernel modules: iwlwifi
```

At this point I knew that I needed a firmware update. Eventually I would have to
run `$ sudo pacman -Syu linux-firmware` (unsure where I found out I needed
linux-firmware specifically) but to do this I need to be connected to the
internet. Thankfully I found an ethernet cable at home. So now I just needed to
figure out how to connect to the ethernet. Apparently many distros have it set
up so that you can connect the cable and it just works. This was not my case.
After a lot of searching around I found that I had to run something like `# ip
link set enp0s31f6 up`. I may have used `modprobe` too but I'm not sure if it
was useful at all.

Here are some of the resources I consulted in the Arch Wiki: [network
configuration][arch-network-config], [/ethernet][arch-ethernet],
[/wireless][arch-wireless]. I had also consulted a few answers on Stackoverflow
and on the Arch forum under the Newbie corner but unfortunately I don't remember
which ones were helpful. I think these notes are enough to kind of guide me (and
maybe others) whenever this happens again.

Anyway this is as much as I remember. Another thing that was important was to
take a break. I got pretty upset when this happened because I was in the middle
of something. I hadn't eaten so that wasn't helping. _I just want to finish this
ONE thing_ I had said to myself and then this happens. I took some time to get a
cup of coffee and some food which really helped me change my mindset from
thinking of one problem and switching to another.

[arch-wireless-rfkill]: https://wiki.archlinux.org/index.php/Network_configuration/Wireless#Rfkill_caveat
[arch-network-config]: https://wiki.archlinux.org/index.php/Network_configuration
[arch-wireless]: https://wiki.archlinux.org/index.php/Network_configuration/Wireless
[arch-ethernet]: https://wiki.archlinux.org/index.php/Network_configuration/Ethernet
