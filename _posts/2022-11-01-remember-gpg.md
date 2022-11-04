---
layout: post
title:  "Remember gpg"
date:   2022-11-01 13:08:17 -0500
categories: [ gpg ]
---

Well, it's that time of year again. Where I've mostly forgotten I have gpg keys
set up somewhere and my system is subtly being weird, and then some software
tells me explicitly:

```
gpg: WARNING: Your encryption subkey expires soon.
```

Oh. Right. Thanks.

I seem to always forget the commands. And sure, I could read the `man gpg` and
figure it out again in the future. It's simple enough. But I just want the
operations in order. So this post is basically my notes for next time.

```
$ gpg --list-secret-keys

/path/to/.gnupg/pubring.kbx
---------------------------------
sec   rsa2048 1955-11-05 [SC] [expired: 2022-10-26]
      0123456789ABCDEFGHIKKLMNOPQRSTUVWXYZ9876
uid           [ expired] Aname <and@email.com>

$ gpg --edit-key Aname
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

sec  rsa2048/OPQRSTUVWXYZ9876
     created: 1955-11-05  expired: 2022-10-26  usage: SC
     trust: ultimate      validity: expired
ssb  rsa2048/41PH4NUM3R53R135
     created: 1955-11-06  expired: 2022-10-26  usage: E
[ expired] (1). Aname <and@email.com>

gpg> expire
Changing expiration time for the primary key.
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 365
Key expires at Thu 26 Oct 2023 01:35:00 AM EST
Is this correct? (y/N) y

sec  rsa2048/OPQRSTUVWXYZ9876
     created: 1955-11-05  expired: 2023-10-26  usage: SC
     trust: ultimate      validity: ultimate

ssb  rsa2048/41PH4NUM3R53R135
     created: 1955-11-05  expired: 2022-10-26  usage: E
[ultimate] (1). Aname <and@email.com>

gpg: WARNING: Your encryption subkey expires soon.
gpg: You may want to change its expiration date too.
gpg> key 1

sec   rsa2048/OPQRSTUVWXYZ9876
      created: 1955-11-05  expired: 2023-10-26  usage: SC
      trust: ultimate      validity: ultimate

ssb*  rsa2048/41PH4NUM3R53R135
      created: 1955-11-05  expired: 2022-10-26  usage: E
[ultimate] (1). Aname <and@email.com>

gpg> expire
Changing expiration time for a subkey.
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 1y
Key expires at Thu 26 Oct 2023 01:35:00 AM EST
Is this correct? (y/N) y

sec   rsa2048/OPQRSTUVWXYZ9876
      created: 1955-11-05  expired: 2023-10-26  usage: SC
      trust: ultimate      validity: ultimate

ssb*  rsa2048/41PH4NUM3R53R135
      created: 1955-11-05  expired: 2023-10-26  usage: E
[ultimate] (1). Aname <and@email.com>

gpg> save
```

Don't forget to save!

