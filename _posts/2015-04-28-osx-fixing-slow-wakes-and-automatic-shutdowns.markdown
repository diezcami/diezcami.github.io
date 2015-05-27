---
layout: post
title: "OSX: Fixing Slow Wakes and Automatic Shutdowns"
date: 2015-04-28 14:29:21 +0800
---
All these commands have been personally tested on my Macbook Pro running OSX Yosemite 10.10.3.

**Slow Wakes** are implemented by default in OSX to maximize the lifespan of a machine's battery, which to my knowledge is more difficult, if not impossible to replace in Apple's newer product lines. On the other hand, **Automatic Shutdowns** are a result of Apple complying with the European Energy Standards, as seen in the following text from their official documentation:

> With the release of the OS X Mountain Lion v10.8.2 supplemental update 2.0, a new feature was introduced to enter safe sleep after four hours of the computer being connected to AC power. This is an effort to comply with the European Energy Standards (ErP Lot6). This will only occur if there is no wireless or Ethernet activity and no activity from external devices such as USB storage devices. 

Depending on when and how you work, however, these features may get in the way of your productivity to the point where the benefits they bring to your machine's battery are negligible compared to its disadvantages.
If you're like me and use your machine daily for work or whatnot, you've probably started seeing these features in a negative light. If you've troubleshooted your system preferences to no avail, you'll most likely have better luck tweaking the **Power Management Settings** of your machine, which can be accessed through the Terminal with the following command: 

```
sudo pmset -g
```

After typing the command, input the password you use to log in and out of your Macbook, and hit `return`. If everything checks out, your screen should show the actual configurations of your machine, as seen below.

``` 
Active Profiles:
Battery Power        -1
AC Power		     -1*
Currently in use:
standbydelay         10800
standby              1
womp                 1
halfdim              1
hibernatefile        /var/vm/sleepimage
darkwakes            1
networkoversleep     0
disksleep            10
sleep                0 
autopoweroffdelay    172800
hibernatemode        3
autopoweroff         0
ttyskeepawake        1
displaysleep         10
acwake               0
lidwake              1
MacBook-Pro:~ Cami$ 
```

What `pmset` shows, in a nutshell, are your configurations for standby, hibernation, sleep and power. Note that these numbers won't be accurate as I've already configured them on my own; the actual settings, however, should be more or less identical. We'll be using these configurations primarily to address the problems brought upon by the features I've mentioned in the beginning of this post.

## Fixing Automatic Shutdowns
The automatic shutdown 'feature' proved to be detrimental to me as I had to rearrange and reopen my windows daily (sometimes bidaily) and check for any lost data prior to putting my machine into sleep mode. I've tried resetting the SMC and NVRAM to no avail, along with tweaking some settings in System Preferences that haven't been touched before the behaviour started. We'll be using `pmset` to solve configure the settings for this feature, as seen below.

The `autopoweroff` line refers to whether your system automatically shuts down or enters the 'safe sleep mode' after being in ordinary sleep mode for the number of seconds specified in `autopoweroffdelay`. Since Apple enabled this feature by default, the value in your terminal for `autopoweroff` will be `1`. To disable it, the value needs to be changed to `0` with the following command:

```
sudo pmset -a autopoweroff 0
```

Despite using this command, however, I found that the auto-sleep behaviour still persisted on my Macbook. If you want to stay on the safe side, I recommend you tweak your configurations for the `autopoweroffdelay` setting as well.
The default value for `autopoweroffdelay` is 14400, which is equivalent to 4 hours as stated in the official documentation. If you're not interested in having your machine shut down automatically in the middle of the day, you can tweak the time value for this setting by using the following command:

```
sudo pmset -a autopoweroffdelay 172800
```

I changed the delay from 14400 to 172800, which is equivalent to 2 days. You can change time value to whatever suits your working habits using the same command as many times as you'd like. The two commands above should cover your issues concerning automatic shutdowns using `pmset`; if you still have problems, you may want to check your **System Preferences** for scheduled shutdowns.

## Fixing Slow Wakes
The other common problem (or battery saving feature, depending on how you look at it) is the slow wake. This happens when your Macbook takes a while to boot up after opening the lid, and can be fixed by editing the configurations stored in `pmset` as well.

When going into standby mode, your computer stores the contents in its RAM into the Hard Drive in order to save battery. Booting up from the hard drive, however, takes time (even for Solid State Drives or Flash-Based Storage) compared to doing so from RAM, which causes the slow boot-up. If you're fine with sacrificing battery life to get rid of this feature, you can turn it off with the following command:

```
sudo pmset -a standby 0
```

I don't recommend this though, as leaving your Macbook unattended for long periods of time with this setting may cause the battery to drain faster and go through more cycles, resulting in lowering its lifespan. A more reasonable compromise would be setting up a time before standby mode kicks in, which can be set by typing the following command:

```
sudo pmset -a standbydelay 43200
```

This tells your computer to remain off standby mode for 12 hours after being put into sleep mode, which allows you to have fast wakes when you open your Macbook as soon as you wake up, assuming you stopped using it right before going to bed. Unlike the former command, however, this setting allows you to compromise your battery less while achieving similar results, depending on how you work. Like `autopoweroffdelay`, however, this delay time can be set to anything, so feel free to tweak the commands.

---

All the commands mentioned in this post will remain after shutting off your machine, so there's no need to do the procedures after every boot-up. You can always confirm the settings by calling `sudo pmset -g` in Terminal. I've covered most of what you need to know to fix the most noticeable sleep and wake issues implemented by default in OSX - if you want to mess with the other variables, you can read up on them [here](http://en.wikipedia.org/wiki/Pmset).