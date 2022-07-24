---
layout: post
title:  "Exif? As if!"
date:   2022-07-23 16:08:17 -0400
categories: [ images ]
---

I don't know about you but I'm wary of _Upload Image_ buttons. I've heard enough
stories and read a few security articles shared on YackerNews, that I am
concerned and have trust issues.

Yet there are some occasions when we want to upload photos. It's nice to share
stuff with friends and get that sweet, sweet dopamine hit when they like it. And
heck yes I want people to upload photos of their purchases so I can have
something else than spurious, over-edited marketing images that dissimulate dumb
angled pockets or whatever weirdness a product has. (YES I'M STILL UPSET ABOUT
THAT STUPID COAT!!).

But what are they doing with the image exactly? Scanning the background to see
your location? Reading any text laying around in the image? Could be! The
technology exists! Some of the information is even stored on the image itself by
way of Exif data. So what is it?

## The EXIF standard

[Exif][wiki-exif] stands for Exchangeable image file format. It's a standard developed in
1985 by the JCIA (Japan Camera Industry Association), the predecessor of CIPA
(Camera & Imaging Products Association). The standard is used to specify formats
for "images, sound, and ancillary tags used by digital cameras (including
smartphones), scanners and other systems handling image and sound files recorded
by digital cameras".

Basically this means that specific information is going to be attached to the
image or audio recording taken with a digital device. You can see examples of
data collected on the [Example section][wiki-exif-ex] of the Wikipedia article.
You see things like Manufacturer, Model, Focal length, etc. But (absent in the
examples) you can also have things like GPSLatitude, GPSLongitude,
GPSAltitude...

Talk about being specific! If you want to have this information on your images,
that's fine. But a lot of it is saved by default. Users are generally unaware
it's even happening. And maybe some people want the convenience of having the
location tagged when they share an image. But from my point of view this
behavior should be 'opt-in'.

So what can we do about it?

## Just use Magick

[ImageMagick][imagemagick] that is. [ImageMagick][wiki-imagemagick] "is a free
and open-source cross-platform software suite for displaying, creating,
converting, modifying, and editing raster images". You can use it to resize
images, to crop them, and so many other things, [checkout their Usage
page][imagemagick-usage].

Now I gotta say, I don't use this program _that_ often. I generally have
Location off, and have adjusted settings to save the least amount of
information. Even so I know that a lot of sites already have a bunch of
information on me since they have other ways of knowing where I'm logging in
from. So if I'm uploading an image on an app I use regularly, I won't bother.
But if I'm uploading a product image on a site I used once, I usually pass it
through ImageMagick.

Following are the commands I use most often. One thing to note is that if you
use the `convert` command, it _WILL_ recompress your image. This doesn't really
matter to me but it's something to keep in mind depending on your future
intentions for the image.

```
# I use this to check what data is attached to the image:
$ magick identify -verbose path/to/image.jpg

# You can actually omit magick and just type the following:
$ identify -verbose path/to/image.jpg

# You can pipe it to grep and check only for exif
$ identify -verbose "[path to image]" | grep "exif"

# This command removes the Exif data, 
# and WILL recompresses the file
$ convert <input file> -strip <output file>

# Using this command will overwrite the original image file
# unless you change the file suffix with the -format option
$ mogrify -strip /example/directory/*

# a one line script to go through all your images
$ for image in IMG*.jpg; do convert "$image" -strip "$image"; done
```

I don't upload things that often so I keep forgetting the commands. This post is
basically a reference for my future self. Maybe it'll be useful for you too!

[wiki-exif]: https://en.wikipedia.org/wiki/Exif
[wiki-exif-ex]: https://en.wikipedia.org/wiki/Exif#Example
[imagemagick]: https://imagemagick.org/index.php
[imagemagick-usage]: https://imagemagick.org/Usage/
[wiki-imagemagick]: https://en.wikipedia.org/wiki/ImageMagick
[wiki-exif-security]: https://en.wikipedia.org/wiki/Exif#Privacy_and_security
