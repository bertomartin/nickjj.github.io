---
layout: post
title: 'Save Yourself Years of Turmoil by Using Docker Today'
tags: [docker, devops, dev-environment]
excerpt:
  Understand the problems Docker solve and how it will potentially save you
  years of headaches by following a time-line of a fictional developer.
---

So, you're either a web developer or are looking to become one and you have a
million questions and uncertainties about how to set up your development
environment or host your applications in production -- I get it.

This article is going to unwind a time-line of a fictional person who is new to
web development. It will cover both development and production scenarios.

By the end of the article you'll understand what problems Docker solve and how
it will potentially save you from years of headaches.

Nearly everything you're about to read is based on real world personal experience
and most of it applies to all programming languages.

### This article is written from the POV of a fictional person

While it will be written in the first person, I will interject my own comments
occasionally in italics. I will also estimate the amount of time someone would
spend while figuring out a specific topic.

##### Here's the back story of our fictional hero:

It's been a long journey but after months of hard work you've gotten to the
point that you're ready to create your first web application.

You know just enough Python and Ruby to be dangerous but you haven't gotten
around to setting anything up yet. You're just about to start your adventure.

Up until now, you've learned everything in a sandbox environment.

### TOC

- [Do I need to switch operating systems?](#do-i-need-to-switch-operating-systems)
- [Time for a new laptop](#time-for-a-new-laptop)
- [Which Linux distro should I use?](#which-linux-distro-should-i-use)
- [Time to install Rails so I can code my Rails application](#time-to-install-rails-so-i-can-code-my-rails-application)
- [My app needs a database](#my-app-needs-a-database)
- [My app needs Redis](#my-app-needs-redis)
- [Wait, Virtual Machines are actually good?](#wait-virtual-machines-are-actually-good)
- [Back to the drawing board](#back-to-the-drawing-board)
- [My friend told me to try Vagrant](#my-friend-told-me-to-try-vagrant)
- [Vagrant is a steaming pile of garbage](#vagrant-is-a-steaming-pile-of-garbage)
- [I want to show the world my app](#i-want-to-show-the-world-my-app)
- [Switching web hosts](#switching-web-hosts)
- [Configuration management tools](#configuration-management-tools)
- [My website just got hacked](#my-website-just-got-hacked)
- [It's been a long road and I want to help my friend](#its-been-a-long-road-and-i-want-to-help-my-friend)
- [Is there a better way?](#is-there-a-better-way)
- [Informing my friend of Docker](#informing-my-friend-of-docker)
- [Converting my Rails app to use Docker](#converting-my-rails-app-to-use-docker)
- [Docker works in production too](#docker-works-in-production-too)
- [How could I have saved all that time with Docker from day 1?](#how-could-i-have-saved-all-that-time-with-docker-from-day-1)
- [Docker takeaways](#docker-takeaways)

### Do I need to switch operating systems?

Most tutorials I found on Google don't mention how to set up Python or Ruby, or
if they do it's for OSX but I'm not using OSX. I'm on Windows.

Almost everyone I talk to says Windows sucks for development so I'm not sure
what to do. Money is tight and I'm not ready to spend $1,500 on a Macbook Pro.

After hours of Googling I managed to learn about Virtual Machines and installed
Linux but I don't like it, it's slow and it runs in a small window.

<p class="underline small">10 hours spent on research.</p>

*A newbie at this stage in his development career won't know about things like
seamless/unity mode or how to properly configure a VM.*

*If you want to learn how, check out my post on 
[how to create an awesome Linux development environment](http://localhost:4000/blog/create-an-awesome-linux-development-environment-in-windows-with-vmware){:target="_blank"}*.

### Time for a new laptop

I'm on a mission to buy a decent laptop to run Linux on. It should be good
enough for development but I'm not quite sure what I'll be running yet.

After trolling Google for hours I managed to find an Acme Inc. laptop for $600.
It has 8GB of RAM, an Intel i5 quadcore and an SSD. This looks good enough.

<p class="underline small">6 hours (16 total) spent on research and spent $600</p>

### Which Linux distro should I use?

I blindly followed a VM tutorial from before which installed Ubuntu but what
else is there? I don't want to have to format again later on if there's something
better.

<p class="underline small">10 hours (26 total) spent on research</p>

It looks like xubuntu is pretty nice. It uses less resources than Ubuntu and
installing things on it is compatible with Ubuntu. I'm sold.

<p class="underline small">6 hours (32 total) spent on research</p>

xubuntu is finally installed and configured in a reasonable way. Time to tweet
about how I'm now an official Linux user. YES!

### Time to install Rails so I can code my Rails application

Time to crack open Google and figure out how to do this.

<p class="underline small">4 hours (36 total) spent on research</p>

I don't get it. So many people use rvm, but a lot of people also say to try
rbenv and then there's an entire camp of others who say to use chruby.

Jesus christ, all I want to do is code my application. I guess I'll pick rvm
because it's what most people are saying to do.

*If you're not a Ruby developer, replace these with virtualenv or whatever
runtime versioning tool your language uses.*

<p class="underline small">6 hours (42 total) spent on research</p>

Finally, rvm is installed and set up. Man, there's so many little things about
Linux that I'm clueless on. I think I'm in over my head but I'll continue
onwards because it works for now.

### My app needs a database

The Ruby on Rails crowd really like Postgres, so it looks like I need to run
Postgres on my laptop.

<p class="underline small">2 hours (44 total) spent on research</p>

Yay, Postgres is installed and my Rails application can connect to it. I wonder
tho, do I need to always keep Postgres running, even when I'm not developing?

<p class="underline small">1 hour (45 total) spent on research</p>

Looks like I need to remember to stop the Postgres service when I'm done coding.

### My app needs Redis

My app has a chat component to it and Rails 5 recommends that I use Redis. Now
it looks like I need to install Redis.

This should go faster because I have a better idea on how to install things on
Linux.

<p class="underline small">1 hour (46 total) spent on research</p>

Cool, the latest version of Redis is installed and everything is working as
planned.

### Wait, Virtual Machines are actually good?

Since I have a laptop, I've been hanging out at Starbucks recently and also
grew a mustache. While twirling my mustache I came across [this post](http://localhost:4000/blog/create-an-awesome-linux-development-environment-in-windows-with-vmware){:target="_blank"}
and it changed my opinion on VMs.

Luckily it's only been 2 weeks, and the laptop can still be returned but I need
to put Windows back on it.

<p class="underline small">2 hours (48 total) spent on research</p>

Finally got Windows back on it, and it's been shipped back. They told me I'll
get my $600 returned in about 10 days. Whatever, that works for me.

### Back to the drawing board

I know what I want to install, but now I need to do it again. Hopefully I can
crank this out quickly.

I just need to find the posts I followed before because I don't remember all of
the commands I ran the other day.

<p class="underline small">6 hours (54 total) spent on research</p>

xubuntu is now running in Unity mode with vmware and my Rails app is back to
working. This is so much better than before, I wish I knew this earlier.

### My friend told me to try Vagrant

He mentioned how Vagrant is the future and that I should be using it instead of
my current approach because it will let me share my set up with other developers.

Honestly, I don't care about that right now. I mean, my set up is working well
but I'll try Vagrant because not future proofing myself sounds scary!

<p class="underline small">6 hours (60 total) spent on research</p>

I think I understand what Vagrant is now and it does seem like it could be good.

My vmware based set up is great for me, but if I want to create a repeatable
environment for others then Vagrant seems like the way to go.

### Vagrant is a steaming pile of garbage

<p class="underline small">10 hours (70 total) spent on research</p>

I don't get it. I set up a shared folder but every once in a while my CSS and
JS files get garbled and they don't get updated.

The only way to fix it is to re-create and restart the VM which takes forever.
I can't believe people actually use this software in real life.

I've wasted so much time on this. Google says I should try to use something
called NFS but it looks like it's a lot of trouble to get working on Windows.

I'll give it a shot tho...

<p class="underline small">4 hours (74 total) spent on research</p>

Well, it's back to working now and I haven't gotten any of the CSS/JS issues
since but that was brutal to set up.

*While we're at only 74 hours total, it's not like someone moves through all
of this in 74 hours. This is likely 6 months of real life time or more while
they figure things out.*

### I want to show the world my app

I've given up on Vagrant and spent a lot of time coding my app and now I am
ready to show the world the fruits of my labor.

<p class="underline small">25 hours (99 total) spent on research</p>

The amount of crap I had to research to get my app on a live server was absurd
and I barely scratched the surface.

I just blindly followed some tutorial but now I have my app running on a live
server. I have no idea if it's secure, but it works.

During my research I read about Heroku, and this did look a lot easier but it
was way too expensive for what I want to do.

Right now my main problem is I have no idea how to update the application.

<p class="underline small">10 hours (109 total) spent on research</p>

I can update the app now with Capistrano but I really have no idea what I'm doing.

### Switching web hosts

I just learned that AWS has a free tier and free is better than not free, so it's
time to jump ship.

<p class="underline small">15 hours (124 total) spent on research</p>

I manually set up the instance on AWS and things are working again but I really
dread having to do this again.

I wonder if there are any tools I can use to help me in this department.

### Configuration management tools

<p class="underline small">60 hours (184 total) spent on research</p>

It looks like there's a lot of tools I can use. I read about Puppet, Chef,
Ansible and SaltStack.

I spent a lot of time watching video guides, reading tutorials and trying things
on my own. It's hard to say which one I like best.

Ansible had the least amount of complexity and it seems to solve the problem of
wanting to create new servers with certain software installed and configured.

*Chances are this section alone was months of real life time.*

### My website just got hacked

Well, that sucked. I guess my server wasn't very secure because I woke up today
and noticed someone trashed my server.

All of my data is gone, and I can't even get back into my server. I tried to
contact support but it's been days without a response.

Time to delete my instance and read up on security and backups.

<p class="underline small">30 hours (214 total) spent on research</p>

I finally get where I went wrong, but my long research sessions have paid off
because now I know how to secure my server and perform database backups.

### It's been a long road and I want to help my friend

It's been well over a year now and one of my friends wants to get into programming.

He is running a Mac and asked me if I could get him situated and at the point
where he has Rails installed.

<p class="underline small">8 hours (222 total) spent on research</p>

It took us all day but we got it running. OSX is so much different than Linux,
but on the bright side we got Postgres and Redis running too.

He even likes my app so much that he asked if he could help code it with me
once he learns more. I like this idea, but it also reminded me of what my other
friend said about Vagrant months ago.

Maybe I'll open source my app, and other developers will want to contribute.
There's no way I can expect them to spend hours setting up their development
environment just to run my project.

### Is there a better way?

Having being burnt by Vagrant in the past, I would like to find an alternative.

<p class="underline small">15 hours (237 total) spent on research</p>

There's this thing called Docker that helps in this area. It allows you to
package up an application or service with all of its dependencies into a
standardized unit.

I have no idea what this really means but I saw a working demo and it looks
awesome.

<p class="underline small">1 hour (238 total) spent on research</p>

After getting it installed I was able to blindly run commands and spin up a
complex example web application in minutes.

It almost seemed too good to be true. It was so easy to install on Linux.

There has to be a catch right? There's always a catch!

### Informing my friend of Docker

I went to my buddy's place and told him about Docker. We installed it on OSX
together.

<p class="underline small">2 hour (240 total) spent on research</p>

It wasn't as easy as Linux and it was definitely different, but it wasn't bad
at all compared to the alternatives.

I also noticed on Docker's site that the experience for OSX and Windows will be
improved in the future by [allowing Docker to run natively on those platforms](https://blog.docker.com/2016/03/docker-for-mac-windows-beta/){:target="_blank"}.

### Converting my Rails app to use Docker

<p class="underline small">20 hour (260 total) spent on research</p>

There was a lot to take in but I converted my app. I'm now able to spin up the
entire app in about 2 seconds and shut it down at will.

The development experience is awesome and I feel like I can carry this knowledge
over to any programming language that I use.

More importantly, my OSX friend was able to get it running well too.

I'd feel very confident pointing other developers to Docker if I decide to open
source my app. I just need to solve the production problem now.

### Docker works in production too

<p class="underline small">10 hour (270 total) spent on research</p>

Well, I'll be damned. After a long day I had everything "Dockerized" in production,
but the big win here is if I changed hosts or had to bring up a new server, I
could do it in minutes not hours.

More importantly, I can be sure that things will work because all of the dependencies
of my app and services have been packed up into Docker images.

### How could I have saved all that time with Docker from day 1?

- **I wouldn't have** had to buy a laptop to install Linux on
- **I wouldn't have** had to research Linux distros
- **I wouldn't have** had to research rvm and friends
- **I wouldn't have** had to learn how to install Postgres and Redis directly
- **I wouldn't have** had to spend time learning Vagrant
- **I wouldn't have** spent a ton of time provisioning production servers manually
- **I wouldn't have** had to spend time configuring my friend's OSX box

- **I would have** still likely learned a bit about configuration management
- **I would have** still needed to learn about security and best practices

All in all, I would have saved hundreds of hours and months of my life if I had
started from Docker from day 1.

### Docker takeaways

Here's 5 things that Docker will help you with today:

##### Cross environment consistency
Docker allows you to encapsulate your application in such a way that you can
easily move it between environments. It will work properly in all environments
and on all machines capable of running Docker.

##### Expand your development team painlessly
You should not have to hand over a 30 page document to a new developer to teach
them how to set up your application so they can run it locally. This process can
take all day or longer, and the new developer is bound to make mistakes.

With Docker all developers in your team can get your multi-service application
running on their workstation in an automated, repeatable, and efficient way.

You just run a few commands, and minutes later it all works.

##### Use Whatever Technology Fits Best
If you're a startup or a shop that uses only one language, you could be putting
yourself at a disadvantage. Since you can isolate an application in a Docker
container, it becomes possible to broaden your horizons as a developer by
experimenting with new languages and frameworks.

You no longer have to worry about other developers having to set up your
technology of choice. You can hand them a Docker image and tell them to run it.

##### Build your image once and deploy it many times
Since your applications are inside of a pre-built Docker image, they can be
started in milliseconds. This makes it very easy to scale up and down.

Time consuming tasks such as installing dependencies only need to be run once
at build time. Once the image has been built, you can move it around to many hosts.

This not only helps with scaling up and down quickly, but it also makes your
deployments more predictable and resilient.

##### Developers and operation managers can work together
Docker's toolset allows developers and operation managers to work together
towards the common goal of deploying an application.

Docker acts as an abstraction. You can distribute an application, and members
of another team do not need to know how to configure or set up its environment.

It also becomes simple to distribute your Docker images publicly or privately.
You can keep tabs of what changed when new versions were pushed and more.

## Ready to learn about Docker?

Check out my Docker related courses:

<div class="container">
  <div class="columns one-half">
    <a href="{{ site.baseurl }}courses/scaling-docker-on-aws">
      <img class="responsive-image course-image" src="{{ site.baseurl }}assets/img/courses/scaling-docker-on-aws-thumb.jpg" width="320" height="180" alt="Scaling Docker on AWS" />
      <h5>Scaling Docker on AWS</h5>
    </a>
  </div>
  <div class="columns one-half">
    <a href="{{ site.baseurl }}courses/docker-for-devops-from-development-to-production">
      <img class="responsive-image course-image" src="{{ site.baseurl }}assets/img/courses/docker-for-devops-from-development-to-production-thumb.jpg" width="320" height="180" alt="Docker for DevOps" />
      <h5>Docker for DevOps: From Development to Production</h5>
    </a>
  </div>
</div>

##### Are you a Python developer interested in Docker?

The
[Build a SAAS App with Flask]({% post_url 2016-03-14-build-a-saas-app-with-flask-is-getting-a-complete-make-over-soon %})
course will also use Docker in development.
