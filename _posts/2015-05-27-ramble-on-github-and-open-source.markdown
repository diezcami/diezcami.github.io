---
layout: post
title: "A Ramble on Github and Open Source Development"
date: 2015-05-27 02:34:25 +0800
--- 
While I spent the past month studying C++, I also took the time to look into **Github** a little more seriously in order to improve my profile as a developer. I realized it's been exactly a month since I published my first commit, and thought it wouldn't be a bad idea to document my experience with Github so far.

## Github: First Impressions
I first encountered Github (more specifically Github pages) when 2048 and its variations first became viral in 2013, however had no idea of its actual purpose then. I made an account a year later in June 2014 when I heard of its relevance to programming, and gave up shortly after creating my first repository as I had no idea where to go next. 

## Installing Octopress
In the summer of 2015, I encountered a blog that ran on [Octopress](http://octopress.org) and thought it was pretty cool primarily for two reasons - one being the framework being targeted to programmers, and the other being my aversion to Wordpress/Tumblr despite wanting to start a blog of my own. With that, I returned to Github with a concrete goal and began attempting to deploy my blog.

The installing instructions were really simple and straightforward - all I needed to do was to install several dependencies and run a few commands on the terminal. At this time, I wasn't 100% familiar with what I was doing, but knew enough to get by and managed to get all the files installed in a local directory. The problems arose when I tried deploying my blog to Github Pages without fully knowing the fundamentals of Git.

I say fully knowing because I was somewhat familiar with Git - I figured `git add` was self-explanatory, and other commands like `git commit` and `git push` seemed pretty straightforward. What I didn't know then was how Octopress had **gems** that actually did the deploying for me, and how the only time I had to use Git commands at all was to push files to the source branch for version control (which I also did not understand then). I had no idea how branches worked then, and ended up typing several Terminal commands that only deepened the hole I dug for myself. By the end of the day, I ended up with mismatched heads, branches that weren't in sync and a 404 page on my blog domain. 

![]({{ site.baseurl }}/resources/images/2015052701.png)

After a while, I realized what `rake deploy` was for, and that actually I didn't need to manually push anything to the master branch. After finally deploying my blog and tweaking its HTML/CSS, I started writing posts once a week and familiarizing myself with Git syntax once again with much less confusion and a more thorough understanding of what I was doing.

## Github: Second Impressions
After being more comfortable with Git syntax, I thought I'd browse repositories and find projects I could contribute to - afterall, it's what Github's primarily for, right? I found a few projects I was interested in such as Atom, Bootstrap and even Octopress. I looked into the source codes of each and every project I was interested in, and (in retrospect, almost unsurprisingly) failed to understand them in every attempt. 

I was dumbfounded. I had always thought of myself as a decent programmer after consistently getting B+/A's in my courses and taking the initiative to study new languages and frameworks in my free time. My world turned upside down when I spent hours looking for projects that weren't ridiculously out of my league, only to end up with nothing on the table.

After freaking out and being mopey for a while, I finally got my act together and started looking into my options - I could continue looking for a repository I had a chance of contributing to, or continue learning languages systematically. I realized, however, that having a good hold on several languages did not help me much with understanding what was going on in the repositories, and figured actually applying my programming knowledge would help me improve more than investing time in any kind of studying or preparation. 

## Pull Requests
I figured by then that I'd have better luck starting out with smaller projects, so I began my search once again with more reasonable expectations. Eventually, I found an interesting [repository](https://github.com/swapagarwal/SaveURLtoDropbox) that  was functional, remotely useful and didn't have a huge base of branches and source codes. Upon inspecting the repository, however, I thought that the programming-related codes actually did not need any refactoring or additions, as the project's end-goal had already been reached. My chance to step in as a contributor came when I visited the project's home page, which at that time had nothing but two input boxes, a button and a footer.

The homepage was technically fine, but I felt it could've used a bit more design outside the default configurations of Bootstrap. I figured why not, forked the repository, and started coding a basic layout - I added a footer that sticks to the bottom of the page, edited a few colors, and added a header to make the site less plain. I submitted the updated HTML/CSS files through a [pull request](https://github.com/swapagarwal/SaveURLtoDropbox/pull/3), and went on with my day not expecting a response or a merge notification. To my surprise, the project author actually replied to clear a few things up regarding copyrights, and eventually merged the pull request. I had finally made my first open source contribution on Github, and it felt great!

After dipping my feet into contributing on Github, I began looking for repositories once again with a more optimistic outlook. At this point, I didn't want to just contribute to repositories - I wanted to actually be involved in a project's development process. I found a project called [thefuck](https://github.com/nvbn/thefuck), a somewhat popular application written in Python that corrects your last console command with the alias `fuck`. I had a little more difficulty contributing to this project, as I had to set up dependencies, work my way around a mid-sized project and figure out how to actually begin contributing my code.

I submitted my second ever [pull request](https://github.com/nvbn/thefuck/pull/216), which addressed issue brought up by another developer. The code I wrote wasn't as optimised as I'd wanted, and I wrote a whole paragraph asking how I could implement the code I originally wanted to use without raising errors. To my surprise yet again, the author replied an hour later saying 'Thanks!', merged the request, and probably went on with his life.

![]({{ site.baseurl }}/resources/images/2015052702.png)

All the work, frustration and hours I had invested into figuring out how to contribute to open source projects finally paid off - and it felt great! Not only did I learn how to use `git pull`, `git merge` and several other commands - I also managed to develop a feature on a project that wasn't mine for the first time, which is a pretty significant milestone for me as a programmer. I fell in love with open source development, and became more dedicated than ever to contribute to an even wider array of projects.

## What Now?
![]({{ site.baseurl }}/resources/images/2015052703.png)

I've only been using Github for a month and have been looking at public repositories for less than a week, so there's a lot of concepts and practices I've yet to learn regarding open source. Despite this, I'm no longer afraid of Git or repositories that're  beyond me, and am instead excited to see what else I can learn from Github. I hope to one day be able to look back at this post with more insights as a programmer and an open source developer.

Thanks for reading!














