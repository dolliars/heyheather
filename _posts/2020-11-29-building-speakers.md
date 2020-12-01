---
layout: post
title:  "Off the wall speakers"
date:   2020-11-29 20:08:17 -0500
categories: [speakers, building stuff]
---

Hey Heather, it's me again.

So I built a set of speakers. Out of ceiling panels. 12x48. They hang on my wall
now. I know. It's kind of amazing that they work as well as they do.

I've wanted a set ever since I was gifted a record player. An expensive thing
for a student though so I kinda forgot about it for a while. But a few months
ago, I came to covet a vinyl and thus I was inspired to fulfill the want.
Initially, I thought I'd get a set of Pioneer Bookshelf speakers which do a
pretty decent job. But then I remembered a Youtube channel I came across when
planning to make banana brandy (more on that in the future). And since we were
going through the summer of our discontent, I thought why not take on a project. 

The channel had put up [these two][YT-speakers-1] [videos][YT-speakers-2] on
making speakers and after watching them, I concluded that building these would
solve many of the extracurricular problems that come with setting up speakers,
all whilst causing additional unanticipated problems. Here's a bit more on that.
Take heed to the fact that I won't be describing the making "How-to" but you'll
get a sense of a few things to look out for if you're ever so inclined to make
your own.

## Decisions

There's a lot fussy logistics surrounding speakers. Before figuring out the
equipment, you need to decide things like: where will they live? How high do
they need to be? Do I need new furniture or can I fashion some out of the
inordinate number of cardboard boxes I have? What distance do they need to be
from the wall? Then you get into the gear: What type of amplifier do I need?
What's the difference between a 16AWG wire and a 12AWG wire? Are they
interchangeable? Wait what? You're telling me there's another
[tweeter][wiki-tweeter] that also has to do with loudspeakers? ... What's a
woofer?

It's pretty amazing. You start with a simple want. *I just want to play a few
records*. Next thing you know you're on [McMaster-Carr][mcmaster-carr] checking
out soldering stations and the various types of [cotter pins][wiki-cotter-pin].
This is the fun part by the way, but I can see how it could be daunting for some
and why it makes all-in-one grab-and-go devices so attractive. Before getting
into any of this, I suggest you list your priorities and constraints. Here was
my list:

1. Good quality sound
2. Compatible with record player, phone, and laptop
3. Minimal surface area footprint
4. `$totalPrice` <= `$pioneerPrice`

My primary concern was sound quality. Ever been to a gathering where someone
decides it's a good idea to play music on their phone? And then someone else
suggests putting the phone in a bowl so it resonates more? Because maybe that'll
help? No one wants that. And I'm sorry I ever suggested it. The point is I've
heard my fair share of unqualified music producers, and I would be remiss if I'd
get them to produce my music.

Next criteria was compatibility. Note the omissions. I didn't care about
portability, surround sound, or television compatibility. As for the surface
area and price, those had some flexibility so I benchmarked them to bookshelf
speakers. This meant that I didn't want anything specialized or that would go on
the floor, and that it shouldn't cost more than the Pioneer Speakers. I gave
myself some leeway on budget so long as the overage was related to acquiring new
tools.

With all that rattling around in me brain, I went back to the videos and decided
that those were indeed the ideal speakers. Sound quality? Check. Compatibility?
Just get the right amp. Surface area? They float! Price? *Check!!*

## Picking a Panel

Watching the videos, all my questions had been answered to a satisfactory
degree. The great thing about this channel is that they're very thorough in
their explanations and demonstrations. Reaallyy practical for [someone like
me][xkcd-1801]. They go over the materials and their characteristics, the sound
tests they ran, and so much more! I took a bunch of notes and after some
deliberation I settled on the following materials for the panels: [extruded
polystyrene][wiki-xsp], hexagonal cardboard, and ceiling tiles. Yeah, I got a
little excited about testing the cheaper materials myself. Unfortunately in my
quest I wasn't able to find the cardboard of all things. I've got the extra gear
to test it should I come across any. Let me know if you get some. In any case,
you'll probably see me eyeing the sidewalks on garbage day. Someone is bound
to be throwing some out!

At this point you might be saying "*what in tarnation are you going on about
with yer ceilin' panels! that don't make no sense!*" To which I would reply "I
can explain! also why are you talking like Yosemite Sam??" Anyway, up to now I
haven't really explained how these speakers are different than conventional
bookshelf speakers. So let me attempt what will certainly be a reductive
explanation. Once again I'll just mention that [the two][YT-speakers-1]
[videos][YT-speakers-2] I linked do a better job.

## Don't phase me out

What's this now about phasing? Bear with me for a minute, we 'bout to get
geometrical. So imagine an equilateral triangle with you at one point, and the
two other points have a single speaker on each of them, which are playing the
same thing. Now if you imagine the sound waves emitted from the speakers,
they'll pretty much be the same and will reach you at the same level. 

Now say you start moving to the left, to the left. And instead of an equilateral
triangle, the shape between the 3 points becomes more like a scalene triangle.
As you're moving, the distance between you and each speaker becomes unequal and
the sound waves will reach you at different levels, one higher than the other.
That is essentially my simplistic explanation and understanding of phasing. If
you continue to move around, there will be a point where the phase shifts enough
so that the sound waves from one speaker reach you at their highest peak and the
other at their lowest. At that point, the sound will cancel itself out and
you'll hear very little amplification. As you move around, you'll hear these
variations in sound amplification.

The reason I'm talking about phasing is because the speakers I've built aren't
of the conventional type so this phasing effect is minimized. What I mean by
conventional speakers are the type that were invented by two people who,
surprisingly, contributed nothing to the cereal world: [Edward W. Kellogg and
Chester W. Rice][wiki-loudspeaker]. In 1924, Kellogg's and Rice crisp sounding
dynamic speakers were born. But the ones that I've fabricated, well they're
[Distributed mode loudspeaker][wiki-DML]. *Don't worry! You won't need to worry
about clocks!* The main difference in how they produce sound is that while
conventional speakers use a forward/backward motion, kinda like a piston, DML
speakers generate random vibrating nodes at different frequencies and amplitudes
throughout the entirety of a surface. So because the sound is coming from the
entire panel instead of a focalized point, and because of the random surface
vibration, there is less sound variation within a room, i.e. there's less
phasing.

That's it. That's all I've understood up to now about the main differences.
There's definitely more information to extract here but this is enough for me to
get a general sense as to why these speakers sound so much better than I
anticipated.

## Hardware words

Moving on to the gear, I got most of the components from [Parts
Express][parts-express]. Note that if you have it shipped to Canada you'll have
to pay import fees. You'll also have to deal with a crummy website to pay the
fees. But you probably deal with crummy sites every day. I know I do! As for the
rest, I went to the hardware store. Having previously visited one where I was
asked "what are you looking for?" only to answer with a blank stare, followed by
weird gesticulation, this time I was prepared. I had my list! I even translated
it in case the clerk was francophone:

- ceiling tile: tuile de plafond
- pink foam insulation: panneau isolant
- plastic bushings: réduit en plastic
- cotter pins: goupilles

How diligent of me. Unfortunately, this was useless. Here's a snippet of the
conversation I had:

> \- Allo! J'ai besoin de goupilles et d'un réduite.
<br>
> \- Un quoi?
<br>
> \- euuhh.. un réduite. En plastique.
<br>
> \- Comme un washer?
<br>
> \- euh. non? ...

*Quesskispasse!* Welp. Back to gesticulating. Which also didn't help. I never
got the right plastic bushings or the cotter pins. I needed to be wayy more
specific. Next time I'm just bringing screenshots. Here I was thinking they
would just direct me to the section, where I could rummage a bit and
serendipitously come across what I needed. No dice.

Communicating about hardware is complicated. In some cases you depend on someone
else to get the necessary item. And if you and your interlocutor use different
terminology, it can make it all the more challenging. Heck, you could be using
the same word but mean different things! So rather than fuss around with
nomenclature, let a picture speak for you. I hear they've got a lot to say.

## Production challenges

It mostly went well. I took a lot of time taking notes and making decisions
first so I knew where everything would go and how I'd assemble it all. The main
issues I had were with puncturing and reinforcing the ceiling tiles, and
soldering the wires to the audio exciters. If I were to do it again, I would
puncture the tile from the front. If you do so, any tear out you have will be in
the back. Reinforcing could've gone a lot smoother. Since I didn't find the
plastic bushing, I cut up a plastic container and made a tiny tube. I used fast
setting epoxy to glue it in place but the tube wasn't exactly the right size and
kept shifting. It worked out in the end, but the results could be much cleaner.

The other difficulty I had was soldering. When I first planned the project, I
had no idea this was required. And now that I'm remembering this, I'd say it's
the part that is lacking in the videos. I got the equipment necessary and
watched _a lot_ of other videos on soldering. They make it look so much easier
than it is. It didn't help that I had the wrong wire gauge. I still managed to
make it work.

The final thing I'll add is: CHECK YOUR MATH! I almost incorrectly positioned
one of the audio exciters!! Simple arithmetic mistakes happen, so be sure to
double check. And write your numbers down. Since the panels were taking up 50%
of my table, I just wrote my calculations on the back because why not. This
turned out to be super helpful because as I was preparing something else, I saw
my quotient and it looked wrong. So I calculated again. And I bet you can guess
by how much I was off. This had skewed the position on both the X and Y axis so
I'm glad I caught it when I did since I had already marked the position.

In conclusion, I now have speakers.

[YT-speakers-1]: https://www.youtube.com/watch?v=CKIye4RZ-5k
[YT-speakers-2]: https://www.youtube.com/watch?v=zdkyGDqU7xA
[wiki-tweeter]: https://en.wikipedia.org/wiki/Tweeter
[mcmaster-carr]: https://www.mcmaster.com/
[wiki-cotter-pin]: https://en.wikipedia.org/wiki/Split_pin
[xkcd-1801]: https://xkcd.com/1801/
[wiki-xsp]: https://en.wikipedia.org/wiki/Polystyrene#Extruded_polystyrene_(XPS)
[wiki-loudspeaker]: https://en.wikipedia.org/wiki/Loudspeaker
[wiki-DML]: https://en.wikipedia.org/wiki/Distributed_mode_loudspeaker
[parts-express]: https://www.parts-express.com/
