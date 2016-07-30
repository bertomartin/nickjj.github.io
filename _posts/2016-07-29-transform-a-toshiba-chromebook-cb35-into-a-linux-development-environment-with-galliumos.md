---
layout: post
title: 'Transform a Toshiba Chromebook CB35 into a Linux development environment with GalliumOS'
tags: [dev-environment, productivity, tutorial]
excerpt:
  Learn how to upgrade and transform a Chromebook to run GalliumOS, which is a
  native Linux based OS designed for Chromebooks.
---

For all of my life I have used desktop workstations for my computing needs and
I have always built them up by parts to get the best performance and value.

This mixed well with my lifestyle. As a self employed course instructor and
consultant, a majority of my work is done remotely. I consider this my home base
and my source of income as well as entertainment.

**I didn't have a need for a portable computing device, or so I thought...**

In case you need to be convinced at how much value one could add to your life,
here's a few quality of life improvements I gained immediately:

- It encourages me to read more because now I can read at night from either my bed or a comfortable chair close to my bed
- Being able to move away from my [standing desk workstation]({% post_url 2016-01-12-build-a-home-made-standing-desk-for-50-dollars-in-10-easy-steps %}){:target="_blank"} helps sparks creativity (working outside and from different locations)
- Productivity has gone way up because of being able to work at different locations (I'll be writing another post about this in the future)
- Every few weeks I take a 90min train ride to NYC for tech meetups, now I have something to do and 3 hours round is a lot of time

### Here's what you'll learn when you read this post

- [How to determine if you want a laptop or a Chromebook](#how-to-determine-if-you-want-a-laptop-or-a-chromebook)
- [Chromebook model recommendation](#chromebook-model-recommendation)
- [Review of the Toshiba Chromebook 2 CB35 (2015)](#review-of-the-toshiba-chromebook-2-cb35-2015)
- [How to swap in an SSD card to your Chromebook](#how-to-swap-in-an-ssd-card-to-your-chromebook)
- [How to install GalliumOS so you can run Linux natively on a Chromebook](#installing-galliumos)

### How to determine if you want a laptop or a Chromebook

When I decided I wanted a portable computing device I assumed I wanted a laptop
because I saw a Chromebook as some type of useless thing that only lets me run
web browser based applications.

The first thing I did was make a list of what I wanted to do with the laptop. In
a previous blog post
[I talk about the value of creating schedules and lists]({% post_url 2016-07-18-schedules-arent-a-constraint-on-life-they-let-you-live-it %}){:target="_blank"}
so making a list was the natural first step.

Here's what I came up with:

- Read e-books
- Use a web browser
- Stream videos
- Do real development work (Docker based non-trivial Rails / Flask apps)
- Create content in written form (I didn't expect to be able to record screencasts)

The most important thing about the above list is I didn't want any of the above
to be much slower than my current i5 / 16GB of RAM / SSD workstation.

If you're a reader of my blog you know that I run Windows but then [I run an
xubuntu VM inside of Unity mode]({% post_url 2016-02-23-create-an-awesome-linux-development-environment-in-windows-with-vmware %}){:target="_blank"} which gives me a full Linux development environment
that runs alongside my Windows OS.

That's the only set up I can run which lets me use high quality screen and audio
recording software while giving me the ability to spend my time in a Linux
environment while still having access to native Windows apps and games.

Ok, enough about that. My point is, I want my portable computing device to feel
very snappy because I don't want to constantly think *"well, I should really go
back to my workstation because it's too slow to work here".*

#### Now that I know what I want, it's time to research laptops

I spent the entire morning researching laptops by reading review sites, watching
Youtube videos and scouring the web to get opinions from other software developers
who were looking to get a laptop.

After nearly half a day of researching laptops I came to the conclusion that
all of them priced in the $300-350 range were not that great.

They suffered from 1 of a few problems, such as having a really low end CPU,
only 2GB of RAM, no SSD, poor displays, poor touchpads and so on.

If you want to jump up to the $550+ price range you can find high quality
components such as an i5 with 8GB of RAM and a 256GB SSD.

For example, [here's one by Acer that has raving reviews](https://www.amazon.com/gp/product/B01DT4A2R4/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=nickjanetakis-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B01DT4A2R4&linkId=496be5e222b6291369c0a393c797c2c0){:target="_blank"} for the most part.

I'm sure it's a fine laptop and realistically I was willing to invest $550 if
it were a great solution but I realized its specs and price point were great
but it conflicts with my interests.

Do I really need such a powerful machine to do what I want? It was like it was
almost good enough to replicate my workstation's set up but not quite.

Also in the back of my head, I was thinking that it would be stupid to try and
replace my workstation because my workstation is great for what it does.

#### Enter Chromebooks

During my laptop research phase I read about how you can run Linux on Chromebooks
and to me that sounded attractive.

Also for the most part, Chromebooks in the $300ish range had much better keyboards,
touchpads and displays found on similarly priced laptops.

I love the idea of running native Linux without having to use a VM like my
workstation. Unfortunately most articles I read pointed to using [https://github.com/dnschneid/crouton](https://github.com/dnschneid/crouton){:target="_blank"}.

crouton sets up a Chroot to run Linux alongside ChromeOS which is Chromebook's
native OS. That sounded cool but I read a bunch of stories about how things just
didn't work quite right, and also for a machine that might be resource constrained
I wanted to ensure I found a native solution.

Then I found [GalliumOS](https://galliumos.org/){:target="_blank"}. Their slogan
really connected me with, which is *"A fast and lightweight Linux distro for ChromeOS devices."*.

Hell yes, that's exactly what I want. Then I learned it was based on xubuntu
which is what I have been using for years and it was like a match made in heaven.

<a target="_blank" href="{{ site.baseurl}}assets/img/blog/galliumos-2-desktop.jpg">
  <img src="{{ site.baseurl}}assets/img/blog/galliumos-2-desktop.jpg" alt="GalliumOS 2.0 Desktop" />
</a>

It's almost too good to be true right? What's the catch?

### Chromebook model recommendation

Most Chromebooks that I saw only had 16-32GB SSDs, or larger non-SSD drives. That
really puts the brakes on your plan to install Linux and set up a proper development
environment.

There's really no way to accomplish everything I wanted with a 16-32GB SSD. I
came across the [Toshiba Chromebook 2 CB35 (2015)](https://www.amazon.com/gp/product/B015806LMM/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=nickjanetakis-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B015806LMM&linkId=d400f068feb7912a7ed42af7e37e754a){:target="_blank"}
and it looked like the perfect device except it only had a 16GB SSD.

Luckily for me I learned that you can just take the thing apart and put in a new
SSD card without too much of a hassle.

Someone who was involved with the GalliumOS project pointed me to [a specific
SSD expansion card](https://www.amazon.com/gp/product/B00KLTPUU0/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=nickjanetakis-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B00KLTPUU0&linkId=91bb6d10027c9167c4dfa2936986b1ee){:target="_blank"}
that was compatible with the Toshiba linked above as well as a few other Chromebooks.
$50 for a 128GB SSD sounds good to me!

So now for about $350 you can have an excellent Chromebook running GalliumOS and
have plenty of disk space. If you really want more than 128GB you can always
buy the other capacities for a bit more money.

If you want a different Chromebook then make sure you check out the
[hardware compatibility guide](https://wiki.galliumos.org/Hardware_Compatibility){:target="_blank"}
on GalliumOS' site because not all Chromebooks will work.

The rest of this post will be based around the Toshiba linked above but most of
the advice can be followed with other Chromebooks that have a Broadwell based CPU.

The next section will explain why I chose the Toshiba Chromebook 2 CB35 (2015).

### Review of the Toshiba Chromebook 2 CB35 (2015)

![Toshiba Chromebook 2 CB35 (2015)]({{ site.baseurl}}assets/img/blog/toshiba-chromebook-2-cb35-2015.jpg "Toshiba Chromebook 2 CB35 (2015)")

First, let's go over its specs:

- 1.7 GHz Celeron 3215U (or an i3 for $45 more)
- 4GB of RAM
- 13.3" 1920x1080 IPS display (165 PPI)
- 2.9 pounds

I don't know about you, but having used an i5 3.2GHz workstation I was skeptical
that a Celeron processor that's not even an i3 would be able to do what I wanted.

While I suffer from an illness called cheapfuck-atitis, I am willing to spend
money when it makes sense and after I talked to a few developers who were using
Chromebooks with a similar CPU I was feeling better about it.

I went into this thinking I'd get the 3215U and if it happens to not be good
enough then I'd return it and try the i3. Spoiler alert: the 3215U is awesome!

#### Testing out a realistic work load

Since I'm a developer and you're probably a developer or into tech at the very
least, let me tell you what I've ran on it to test the performance:

- Google Chrome with 6 tabs open
- Youtube playing back a video (streaming music is important!)
- Docker daemon
- Dockerized Rails app with 28 gems
- Dockerized Sidekiq background work
- Dockerized Action Cable server
- Dockerized Postgres and Redis
- Sublime Text 3 with about 30 plugins
- 2 terminal windows, one with 2 tabs and the other with 3
- 1 PDF open with the native PDF viewer
- A 2nd workspace with another Google Chrome window and 3 more tabs

Result? If I don't touch anything the CPU idles at about 14% and the memory
usage sits at about 60% used. Not only that, it was silent too, awesome!

If I goto Chrome and start browsing sites, it's extremely snappy and pages load
nearly instantly. The Rails application reloads on the order of milliseconds
when I make change codes. Coding feels very snappy too -- there's no hitches.

The only time I noticeably saw worse performance over the workstation was when
native gem extensions had to be compiled. They took a little longer than my
workstation (damn you nokogiri!) but that's a rare event for me.

If you're doing a ton of compiling on a regular basis you may want to upgrade to
the i3 model, but it might be worth testing this one first.

#### Let's talk about the display

One of the main features of this Chromebook is the display. I definitely don't
want to develop with less than 1920x1080 screen resolution, it makes me feel
claustrophobic.

I was a little concerned about 1080p on a 13.3" screen because my primary monitor
was 21.5" at the same resolution. The smaller your screen is, the higher the pixels
per inch will be, which means things will become smaller and smaller.

As soon as it booted up, all of my worries went away. If you have decent vision
then you won't have any problem at this size. I would describe it as very comfortable
to read everything at its native size from a reasonable "laptop distance" but
I wouldn't mind things being a touch bigger.

In other words, for my brain 15" is probably the optimal 1080p resolution but I
have no real complaints or worries with this 13.3" screen. There's no eye strain.

I'm really sensitive to these things usually. Back in the day I used to play
competitive Quake 3 on a CRT at 120hz and I was one of those weirdos who could
tell the difference between 90hz and 120hz.

Oh and don't worry, if you do need to scale it because the text is too small
then it's no problem. The UI can be scaled with very minor display issues.

#### How's the keyboard and touchpad?

The next most important pieces are the keyboard and touchpad. If either of them
suck it could be a deal breaker. Sure you could use external devices but I'm
looking for a convenient device to use in a portable way.

I don't want to have to lug around an extra keyboard or mouse.

One cute thing about the
[Toshiba Chromebook 2 CB35 (2015)](https://www.amazon.com/gp/product/B015806LMM/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=nickjanetakis-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B015806LMM&linkId=d400f068feb7912a7ed42af7e37e754a){:target="_blank"}
is its backlit keyboard. The keys glow in the dark in a non-distracting way.

With cosmetics out of the way, let's get into the important things. I'm actually
writing this blog post on it and other than there being no delete key I haven't
had any issues adjusting to the keyboard.

Obviously my words per minute are slower since it's a brand new layout for me
but I don't feel like I'm battling it, or getting hung up. The keys feel reasonably
responsive but I'm not one of those crazy people who can type at 140 WPM.

I average at about 80 WPM and haven't used a high end mechanical keyboard to
compare it to. All I know is, I'm happy with this keyboard so far.

**The touchpad seems pretty good**. I don't have a lot of experience with laptops
in general so I don't know well it fares against let's say a MacBook Pro.

All I know is, it's 1 surface and it has a click zone on the bottom that pops
loudly to register mouse clicks but it's optional. You can tap anywhere you
want to register a click and the software lets you tune various sensitivities.

It also supports 2 finger scrolling and you can even swipe left/right to navigate
pages in a browser. I'm not a touchpad wizard so there's probably other gestures
that you can do which I haven't discovered yet.

Since I'm a rookie with touchpads I'm definitely struggling a bit but I feel like
this is my fault, not a fault with the device. I could see myself getting used
to it eventually.

#### What's the deal with the webcam and microphone?

Honestly, way better than I thought. I used the built in microphone on it and my
friend told me it sounded really good.

He's an audiophile and audio is very important to me too. I spent about $115 on
a [Blue Yeti Microphone](https://www.amazon.com/gp/product/B00N1YPXW2/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=nickjanetakis-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B00N1YPXW2&linkId=071703fb7f11c2fa73a6961b830da5e1){:target="_blank"}
which is what I use for all of my course recording and he told me this microphone
can hang with it.

It sounds different than the Yeti for sure, but it's not so much that it sounds
a lot worse. It just sounds different.

I won't be recording my courses on this Chromebook's microphone but it's good
to know that I can do a Google Hangouts with high quality video and audio.

This is one of those things where I didn't really pay attention to these
components before purchasing it but I'm pleasantly surprised at the outcome.

#### What type of ports does it have?

It has 1x USB 3.0 port and 2x USB 2.0 ports along with a proper 3.5mm headphone
jack and an HDMI port. That's good enough for me.

It's missing a USB-c port which kind of stinks but it's not a deal breaker.

#### Network speed and speaker quality

The wireless network device is rock solid. My ISP gives me 30MB down and 5MB up
and in a speed test I was getting identical numbers to my wired i5 workstation.

I did a lot of tests for packet loss too and it passes all tests with flying colors.

The speakers are probably the weakest link of everything, but you'll have your
own headphones or earbuds anyways so it's a non-issue.

I mean, it plays sounds but the quality is pretty poor. The speakers are driven
by Skull Candy, which aren't really well known for high end audio.

I'm glad Toshiba decided to cut corners on the speakers instead of more important
components. If you're in the market for headphones, check out my [budget death
metal headphones blog post]({% post_url 2016-01-06-sennheiser-hd-201-vs-sennheiser-hd-202-for-budget-death-metal-headphones %}){:target="_blank"}.

#### Overall build quality?

I don't know. As long as you don't abuse it, I think it will be fine. It's a
little bit flimsy but it's not so fragile that I would feel afraid to actually
use it.

To put things into perspective, I would feel very comfortable putting it into
my backpack in a laptop sleeve and taking trips with it. In fact, I already
rode a bike with it once (inside of the backpack sleeve) and had no problems.

If I dropped it from about head high then I'm pretty certain it would explode
into 85 qaudrillion pieces. Protip: don't drop it.

### How to swap in an SSD card to your Chromebook

If you plan on installing GalliumOS then you'll definitely want to replace the
tiny 16GB SSD with something larger.

The first thing you'll want to do is buy the SSD expansion card. This will
completely replace the 16GB SSD inside of the Toshiba.

I recommend the [Transcend 6GB/s 42mm card I linked before](https://www.amazon.com/gp/product/B00KLTPUU0/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=nickjanetakis-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B00KLTPUU0&linkId=91bb6d10027c9167c4dfa2936986b1ee){:target="_blank"},
feel free to get any capacity you want. I went for the 128GB model.

#### Making a recovery USB stick

The next thing you'll want to do is unbox your Toshiba and turn it on without
making any modifications. Since we're going to be replacing the stock SSD, you'll
want to transfer a bootable copy of ChromeOS over to a USB stick.

This step is only needed if you plan to dual boot with ChromeOS, which is what
I highly recommend. It's worth giving up 6GB or so of your drive for ChromeOS
just to have it around.

1. Grab a USB stick with 4GB+ of available storage and plug it into the Toshiba
after booting into ChromeOS

2. Download the [Chromebook Recovery Utility](https://chrome.google.com/webstore/detail/chromebook-recovery-utili/jndclpdbaamdhonoechobihbbiimdgai){:target="_blank"} Chrome extension to create a recovery USB stick

3. Follow the instructions and once the recovery USB stick is good to go, then shut down and unplug the Toshiba

#### Installing the custom SSD

1. Flip the Chromebook over

2. Unscrew the 8 visible screws on the back

3. Take a razer or something sharp / thin and pop out the 2 rubber stoppers that are furthest away from the vents (they are factory sealed with glue and will take force to rip them out, just try not to rip them in half, they will sit back perfectly after this so don't worry)

4. Unscrew the 2 hidden secret screws that Toshiba decided to troll you with

5. Carefully pry open the case with a butter knife or similar tool to expose its guts (you should not have to use a tremendous amount of force here, [this video shows you how to do it on an older Toshiba model](https://youtu.be/Jh30o8Ud9fo?t=46){:target="_blank"} so it won't look exact)

6. Look for 2 small card slots next to each other and connected by yellow tape. One is the SSD and the one with the wires coming out is the wireless adapter

7. Unscrew the small black screw for the SSD card and gently slide it out

8. Insert the new SSD card (it can only go in 1 way)

9. Screw in the new SSD card

#### Make a judgment call on dual booting

If you plan to dual boot then you can seal things back up, so go do that now.

If you want to install GalliumOS without dual booting you will need to remove
a special write protect screw which will allow a custom firmware build to write
settings to a chip that is normally read only.

You can read more about this on [GalliumOS's firmware page under GBB Flags](https://wiki.galliumos.org/Firmware#GBB_Flags){:target="_blank"}.

I didn't do this personally, because if you dual boot you won't have to use a
custom firmware build with this exact Toshiba model.

### Installing GalliumOS

At this point you should have your new SSD card in. Place the recovery USB stick
in and turn the machine back on. Then enter in your information again if it asks.

#### Entering developer mode

In order to install GalliumOS you're going to have to enable developer mode
which will give you root access to your Chromebook.

To enter this mode with the Toshiba or other Broadwell based Chromebooks:

1. Turn the Chromebook off

2. Hold down `ESC` + `F3 (the refresh key)` and press the `Power button`

3. The machine will boot into a scary looking white screen (don't panic!)

4. Press `CTRL+D` at the white recovery screen

5. Press `Enter` on the "To turn OS verification OFF, press ENTER" screen

6. The machine will reboot and you'll see a "OS verification is OFF" white screen. *This is what you will always see when you turn on your device. Now we're expected to boot into a specific OS. Right now our only choice is ChromeOS.*

7. Press `CTRL+D` to boot into ChromeOS

8. Configure your wifi and other settings

#### Installing GalliumOS

1. Drop into a Virtual Terminal by pressing `CTRL+ALT+F2 (top right arrow)`.  
*If nothing happens then you're not in developer mode, repeat steps 2-5 from above*

2. Login as `chronos` with a blank password

3. If you're using the Toshiba I've been linking and are dual booting then skip this step, otherwise [install a custom firmware](https://chrx.org/#chromebooks){:target="_blank"}

4. Install and run chrx with `curl -Os https://chrx.org/go && sh go` [0]

5. Follow the instructions. *I personally went with the default 114GB partition size with a 128GB SSD, which is reasonable to still play with ChromeOS if you want*

6. Reboot when it asks you to and repeat steps 3-8 from *Entering developer mode* and steps 1-4 from *Installing GalliumOS*
 
This time when you run chrx, it will download and install GalliumOS instead of
setting up the partition like it did the first time.

If your internet connection drops out during the download phase don't worry,
just repeat step 6 in this section.

Everything should complete successfully and you'll have GalliumOS installed.

---

[0] The second time you run this command you may want to include a few flags to
customize your username and/or hostname. You can do that by running:

`curl -Os https://chrx.org/go && sh go -U yourname -H foobarhost`

By default it will create a user `chrx` with a password of `chrx`. If you supply
a custom username with `-U yourname` then your password will be `yourname`.

For a full list of install options check out the [chrx option documentation](https://chrx.org/#options){:target="_blank"}.

**If you forgot to do this step, don't worry.** You can always make a new user or
change your hostname later just like you would in any Linux distro.

For example, after GalliumOS is fully installed you would open a terminal and run:

```
sudo adduser yourname && \
  sudo usermod -a -G adm,sudo,cdrom,dip,plugdev,lpadmin yourname
```

That would ensure your new user belongs to the correct groups. In this case it
would match the default `chrx` user's groups. At this point you would log out
and then log back in and you would be free to delete the `chrx` user.

---

<a target="_blank" href="{{ site.baseurl}}assets/img/blog/galliumos-2-windows-open.jpg">
  <img src="{{ site.baseurl}}assets/img/blog/galliumos-2-windows-open.jpg" alt="GalliumOS 2.0 Windows open" />
</a>

#### For future reference when turning on your Chromebook

If you turn off your Chromebook and boot it up, you'll always be presented with
the white screen. Think of this as your boot menu.

Press `CTRL+L` to boot into GalliumOS or `CTRL+D` to boot into ChromeOS.

If you're wondering why `CTRL+L` was chosen and not `CTRL+G` to better describe
GalliumOS, it's not up to GalliumOS to pick this hotkey. It's something provided
by the firmware.

#### IMPORTANT: If your battery ever drains to 0%, read this

If your battery ever drains to 0% then a certain firmware setting will be
forgotten and it will prevent your Chromebook from being able to boot into
GalliumOS.

This isn't a permanent issue, so don't freak out if you ever hit 0%, however
do understand that you will need perform a few steps to fix the issue.

Fortunately it doesn't take long and since you should rarely hit 0%, you won't
have to worry about it too often. To fix the issue:

1. Boot into ChromeOS (`CTRL+D` at the white screen)

2. Drop into a Virtual Terminal by pressing `CTRL+ALT+F2 (top right arrow)`

3. Login as `chronos` with a blank password

4. Run `sudo crossystem dev_boot_legacy=1`

5. Reboot the system and now you'll be able to boot into GalliumOS with `CTRL+L`

These steps could be bypassed if you removed the write protected screw when
installing your new SSD, but it's not really a big deal to do it this way.

#### Support GalliumOS today

[GalliumOS is an open source project](https://github.com/GalliumOS){:target="_blank"}
and has no commercial backing.

If you think about it, their OS is allowing you to put together an incredibly
useful Linux driven Chromebook for about $350. That's $1,000-$2,000 cheaper
than a MacBook Pro.

If you're enjoying GalliumOS then
[show the developers some love by donating](https://galliumos.org/donate){:target="_blank"}.

### Let me know what you think about GalliumOS

I'd be curious to hear what you think about GalliumOS or the idea of using a
Chromebook to run Linux natively. Leave your comments below.
