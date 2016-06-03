---
layout: post
skip_subscribe: true
title: 'Build a SAAS App with Flask Is Getting a Complete Make over Soon'
tags: [flask, bsawf]
excerpt:
  Build a SAAS App with Flask is going to get a major update in the near future,
  learn what will change and get notified when it's out.
---

##### Update for June 3rd 2016

Everything from last week is complete and I have submit the course for review.

I'm looking to release it Monday, which is June 6th and just as a reminder,
people who are signed up to get notified will receive a limited time discount.

All you have to do is scroll down to the bottom of this page and put in your
e-mail address. When I send out the release notification, you'll be rewarded
with a MASSIVE discount.

This will be the last weekly update for this post. See ya in the course's forums!

##### Update for May 28th 2016

All of the main course's videos are now done and rendered. There's 9 hours and
45 minutes of content.

Here's what's left to do on the TODO list:

- Create quizzes for each section
- Triple check the notes for typos / grammar mistakes
- Write the course landing page text for Udemy and this site
- Create a ~2 minute intro video

It will be a few days to complete the above, then it's up to Udemy to accept
and publish the course which will take anywhere from 3-5 days.

##### Update for May 21st 2016

Sections 15 through 17 are done. That was 41 lectures total.

Here's my TODO list until completion:

- Record and edit 31 lectures spread across 3 more sections
- Render all of the videos (this can be done while sleeping)
- Assemble the entire course on Udemy
- Create quizzes for each section
- Triple check the notes for typos / grammar mistakes
- Write the course landing page text for Udemy and this site
- Create a ~2 minute intro video
- Create a high quality course cover art image

I am confident I can do all of the videos by next week and everything else will
take about another week. Then it's a ~3 business day wait for Udemy to
review the course until it's live.

In next week's update I will have had rendered all of the videos so I'll share
the total length of the course in hours.

##### Update for May 13th 2016

Sections 9 through 14 have been recorded which leaves 7 more sections to go.

So far I've recorded 85 lectures but there's still 70 left to record.

The last 70 lectures have a lot of fairly long lectures so despite having complete
14 of 21 sections I'd say at this point I'm about half way done recording.

There's way more content than anticipated but I was able to record 85 lectures
in 2 weeks so I think I should be able to finish the rest in about 3 weeks.

##### Update for May 6th 2016

The first 8 sections of the course have been recorded, but that doesn't mean I
am over a third of the way done. The earlier sections have a lot less content
than the later sections.

I've released the
[Is Flask Right for You?]({% post_url 2016-05-05-build-a-saas-app-with-flask-free-sample-videos %})
section for free which you can view now.

Also, in case you missed it, here's 2 blog posts that came out of extracting
content from the first iteration of BSAWF:

- [Save Yourself from Years of Turmoil by Using Docker Today]({% post_url 2016-05-02-save-yourself-from-years-of-turmoil-by-using-docker-today %})
- [25 Sublime Text 3 Packages for Polyglot Programmers]({% post_url 2016-04-13-25-sublime-text-3-packages-for-polyglot-programmers %})

##### Update for April 29th 2016

The course is fully planned out. Here's some stats:

- Full compatibility with Python 2 and Python 3
- 21 sections and 156 video lectures
- 15 sections worth of building the app up in stages
- ~4,250 lines of Flask related code (not counting blank lines / comments)
- 108 pages worth of PDF notes that you can reference
- ~97,000 words of course planning notes for myself to help narrate the content

All in all, the above took about 5 weeks to do. I imagine it will be at least
another 5 weeks to record/produce everything but it's too soon to say.

One thing is for sure, I'm happy to be at the point where I can start recording.

##### Update for April 23rd 2016
All of the refactoring from the previous week's update is done and I also added
the last big feature of the app which was to handle processing microtransactions.

My TODO list is quickly shrinking. There's about 10 short lectures left to go
and everything will be accounted for. I also need to make the app compatible
with Python 3 because I want it to work for both Python 2 and 3.

Once that's complete, then I can start producing everything from top to bottom.

##### Update for April 16th 2016
The "game" component of the application has been fully coded. There's 17 sections
at the moment and I think there's only going to be 2 or 3 more sections total.

During this last week I made a decision to remove Vagrant entirely, and also
came up with an awesome new way of writing course notes, so most of this
upcoming week will be refactoring old sections and notes.

##### Update for April 9th 2016
14 sections and 102 lectures have been fully planned out. At this point I have
written 65,000 words of course planning notes.

I would say I'm about 2/3rds of the way done coding the new demo application
and planning everything out.

##### Update for April 1st 2016
12 sections and 67 lectures have been fully planned out. This includes course
planning notes for myself, slides, and notes for students of the course.

---

Honestly, this post is going to be pretty long. Go ahead and get something to
drink, and carve out at least 15 minutes if you plan to read this in 1 sitting.

Yep, this post is so long that it needed a TOC haha.

- <a href="#brief-history-of-the-project">Brief history of the project</a>
- <a href="#whats-been-going-on-since-i-released-bsawf">What's been going on since I released BSAWF?</a>
- <a href="#whats-going-to-happen-with-the-new-version-of-bsawf">What's going to happen with the new version of BSAWF?</a>
  - <a href="#will-existing-bsawf-students-get-the-new-version-for-free">Will existing BSAWF students get the new version for free?</a>
  - <a href="#docker-and-app-deployment-is-being-removed-from-bsawf">Docker and app deployment is being removed from BSAWF</a>
  - <a href="#the-primary-focus-of-bsawf-will-now-be-learning-flask">The primary focus of BSAWF will now be learning Flask</a>
  - <a href="#what-about-webpack-thats-not-a-primary-focus-of-flask-is-it-staying">What about webpack, that's not a primary focus of Flask, is it staying?</a>
  - <a href="#let-me-guess-the-development-environment-stuff-is-getting-pulled-too">Let me guess, the development environment stuff is getting pulled too?</a>
  - <a href="#come-on-why-are-you-pulling-so-much-content-are-you-insane">Come on, why are you pulling so much content, are you INSANE?</a>
  - <a href="#will-catwatch-be-changed-to-a-different-type-of-application">Will catwatch be changed to a different type of application?</a>
  - <a href="#will-the-new-demo-app-still-have-server-side-templates">Will the new demo app still have server side templates?</a>
  - <a href="#will-the-new-demo-app-still-use-bootstrap">Will the new demo app still use Bootstrap?</a>
  - <a href="#will-there-be-a-live-coding-or-a-documentary-style-approach">Will there be a live coding or a documentary style approach?</a>
  - <a href="#if-theres-no-building-up-the-project-then-why-include-it-in-the-name">If there's no "building" up the project, then why include it in the name?</a>
  - <a href="#a-lot-of-people-wanted-an-api-component-so-im-including-one">A lot of people wanted an API component, so I'm including one</a>
  - <a href="#the-courses-structure-will-be-greatly-improved">The course's structure will be greatly improved</a>
  - <a href="#dedicated-notes-for-each-lecture-will-be-included">Dedicated notes for each lecture will be included</a>
  - <a href="#no-more-self-hosted-course-platform">No more self hosted course platform</a>
  - <a href="#how-much-content-will-there-be-and-how-much-will-it-cost">How much content will there be and how much will it cost?</a>
  - <a href="#when-will-it-be-released">When will it be released?</a>
- <a href="#thats-only-the-tip-of-the-iceberg">That's only the tip of the iceberg</a>

### Brief history of the project

During the summer of 2015 I decided I wanted to concentrate my efforts on
creating online learning solutions.

The first set of screencasts I made was
<a target="_blank" href="https://buildasaaswithflask.com/">Build a SAAS App with Flask</a>
and I eventually released that in August 2015.

It was the first time I ever tried producing something like that. The whole
experience of creating a course, editing video and recording audio was new to
me.

I had experience explaining things to people, because part of what I did (and
still do) is consult with people where my job is to listen to them and then
come up with a game plan for executing what they want to do.

However, when it came to producing or hosting a course, I learned as I went.

### What do students think of the original screencasts?

I've had a lot of great feedback from my students. A lot of them said they learned
more than they could ever have expected from going through the content.

My students also come from a very varied background. Everyone from extreme
beginners, to engineers working at Apple, to experienced Flask developers who in
some cases even had a lot of experience doing tech book reviews.

The common trend is that developers with different experience levels were all
capable of absorbing the content and getting a lot of value from it.

Some found it easy, others found it difficult but in the end they learned a lot.

Anyone who has watched the screencasts knows how much is covered. It's not even close
to just Flask. You're getting like 4 courses worth of content built into 1 course.

#### Return rates are hovering at about 1.5%

I'm pretty happy with that result because when I look back at the course's
production quality and structure it actually embarrasses me.

It's embarrassing in the same way as you would be embarrassed when you look at
code you've written when you first started programming.

Also the course was being sold for $200, so it's a non-trivial purchasing decision
for most people. I can only assume that if I did a poor job then more people
would want refunds, but they aren't asking for them.

### What's been going on since I released BSAWF?

Since I've released BSAWF I've went ahead and released a 2nd course which is,
<a target="_blank" href="{{ site.baseurl }}courses/docker-for-devops-from-development-to-production">Docker for DevOps: From Development to Production</a>.

While creating BSAWF I came to the realization that it was too ambitious and
cluttered to try and teach people both Flask and Docker in 1 course.

I also came to the realization that there's a lot of people who want to learn
about Docker but don't really care about Flask and vice versa.

So I extracted out and improved a lot of the Docker material. I based the course
on tactics I've learned over the years for deploying web applications.

It happens to use Flask (and Rails) as example applications to deploy to production
but ultimately the application itself isn't important.

#### Taking the time to learn how to create a course

While making Docker for DevOps I dedicated a lot more time to producing the
course and it definitely shows. I learned the ins and outs of video editing tools.

There were times where I repeated the same phrase 10 times just to make sure it
came out correct. There's very few hard cuts in the course where it's obvious I
cut something out.

#### I've been working on a third course too

For the last few months I've been working on a follow up Docker course that will
go into great detail on how to scale a web application to multiple hosts with
Docker.

It's not out yet, but it will be out very soon. I'm basically just waiting for
my publisher because the content itself has been ready for weeks.

#### What does this have to do with Build a SAAS App with Flask?

The point I'm trying to make is, since I've created BSAWF, I've learned a lot
about creating and producing courses.

I feel like this is a good time to revisit BSAWF and completely re-do it from
the ground up. I love Flask and I can't wait to start doing it.

### What's going to happen with the new version of BSAWF?

Now let's get to the fun stuff. Over the past few months a lot of students have
given me awesome feedback on BSAWF.

I asked you guys a bunch of questions, proposed a couple of ideas and you've
let me know what you want to see changed, added or removed in the next iteration.

I think the best way to handle this is to break down the changes by offering to
organize things in a FAQ-like manner.

#### Will existing BSAWF students get the new version for free?

Yes, absolutely. Existing students are actually going to get a lot of things,
but we'll get into that later.

#### Docker and app deployment is being removed from BSAWF

I'm going to remove most of the Docker content from BSAWF because now if you
want to learn about Docker you can just get
<a target="_blank" href="{{ site.baseurl }}courses/docker-for-devops-from-development-to-production">Docker for DevOps</a>.

However, existing BSAWF students will get Docker for DevOps for free so don't
worry about feeling like you're losing content.

You're gaining a lot here because this course has 7+ hours of Docker goodness,
and explains in great detail on how you can deploy a Flask application to production.

It's much more comprehensive than the book and screencasts I included with the
original BSAWF screencasts.

When I proposed removing the Docker and app deployment content a lot of you
strongly opposed because you really wanted to learn about Docker.

Back when we were spit-balling ideas around, the Docker for DevOps course didn't
even exist so I feel like this is a good compromise.

#### The primary focus of BSAWF will now be learning Flask

It will still use Docker in development, but it's going to be done a lot better
than the current way. I'm estimating you'll be able to get set up in 5 minutes
or less and be able to edit the source code in the comfort of your own OS.

#### What about webpack, that's not a primary focus of Flask, is it staying?

That's a good question. I'll be completely honest with you here. Front end
development is a massive cluster fuck.

I'm still a huge believer in webpack, and I feel like it's a better choice to
use than other tools in the same category.

However, I don't feel like it belongs in the course because it's something that
can be learned independent of the BSAWF material.

Too many students had severe issues trying to implement custom Bootstrap themes
because they have basically no experience with Javascript.

It's information overload to learn about creating a production-grade Flask app
and simultaneously become a Javascript wizard capable of taking a pre-bought
Bootstrap theme with 400kb of JS, and convert that into a webpack compatible way.

I thought about keeping the webpack material in, and then including additional
sections on implementing a custom Bootstrap theme but the fact of the matter
is, each theme requires completely different steps so it's not too useful.

Then there's all sorts of other side topics like, are you going to use server
side rendered templates in your own apps later on, or a single page app with a
dedicated front end framework like React, Angular or Ember.

It's a can of worms that has no business being opened in this course. So now
there will be no asset pipeline that's been built with webpack, and we'll just
include untagged assets directly into templates.

Have no fear, I will curate a free list of webpack resources and will certainly
maintain and improve <a target="_blank" href="https://github.com/nickjj/flask-webpack">Flask-Webpack</a>
in the future because I personally use it in all of my Flask projects.

Perhaps I'll also make a free screencast that transforms the new BSAWF demo app
to use webpack. This way you're in good shape for production.

#### Let me guess, the development environment stuff is getting pulled too?

Yep!

I'm going to be providing less opinions on text editors, general Linux skills,
using tmux and setting up graphical virtual machines.

All of this is stuff is completely out of scope for a Flask course because it
applies to any web framework or development environment.

Now, don't freak out just yet. Sure, I'm pulling this content from the Flask
course but that doesn't mean I'm leaving you dead in the water.

For instance, a few weeks ago I released a free screencast on how to set up
an <a target="_blank" href="{% post_url 2016-02-23-create-an-awesome-linux-development-environment-in-windows-with-vmware %}">awesome Linux development environment on Windows</a>.

There will likely be future posts or screencasts on the surrounding topics of
tricking out your development environment.

So actually in the end, you're going to receive more content than you did before
on this subject matter. It's just that most of it will be free content that
everyone can benefit from.

#### Come on, why are you pulling so much content, are you INSANE?

Well, I might be insane but pulling this content makes a lot of sense. They are
separate topics from Flask entirely.

*In every case you're getting more content than before.*

Think of these topics as side quests in a video game. They are not essential to
completing the main story, but likely have a lot of valuable goodies associated
to doing them.

All of these side quests are going to be either free content for everyone, or
free for existing students because I'm going to give you 100% off coupons. 

#### Will catwatch be changed to a different type of application?

Yes. I still love cats and think it was pretty funny to have a demo application
that streams cat related tweets to paying customers.

It was a fun way to exercise using a payment processor, Twitter's API and
websockets.

However, a pretty decent amount of students kept asking me how to remove all of
the Twitter content because they didn't care about it.

After thinking about this for a while I think it's worth ditching Twitter's API
in the new demo application.

There's still going to be a payment processor and that alone exercises how to
integrate with a third party API. There's no need to integrate with a 2nd third
party API in the demo application, thus Twitter is getting pulled.

I'm honestly not sure what the new demo application will be yet, but it will
definitely still involve using websockets.

#### Will the new demo app still have server side templates?

Yes. I'm a huge believer that most web applications are still document driven,
so it makes sense to use server side templates in the demo application.

Think of sites like GitHub. It's pretty interactive, but at the end of the day
you're just rendering information. The front end can be spruced up by sprinkling
in Javascript when it makes sense.

Plus, in order to learn something like React, we would need to take a huge side
step from learning Flask since they are totally different things.

However, I do want to provide some good news on this front. There will be an API
component added to the new demo application, so if you do want to learn how to
make single page applications with a back end API, then the new version of BSAWF
will teach you how to set up the back end.

#### Will the new demo app still use Bootstrap?

I think so. A majority of people wanted to stick with Bootstrap because it's
pretty much a standard that a lot of front end developers are comfortable with.

Sure, there's nicer looking frameworks, but I want to prepare my students for
things they will encounter in the real world and Bootstrap is winning in terms
of real world popularity.

#### Will there be a live coding or a documentary style approach?

The demo app took almost a month to create off camera and it was the result of
many refactors. It has a few thousand lines of code and quite a few components.

Live coding works well for trivial toy projects, but it really doesn't work well
for a complex real world application.

Let's be honest here, do you really want to sit there and follow along with me
while we code each line together? That approach will end up being over 80 hours
long.

We're living in a world where waiting 400ms for a web page to load induces rage.
Listening to me say "Ok, now type open bracket d i v close bracket" for 10 hours
will bore you to tears.

The bottom line is, a lot of people really enjoyed the documentary style approach
where I gave my thought process on every aspect of the code base.

I like this approach too because now you understand why it's written and have
well commented code to look at as well. It's like getting a private 1 on 1
consultant hunched over your shoulder explaining his thought process to you.

There will still be following along by typing commands and certain bits of coding
but there's not going to be another 3.5 hour live coding session like the first
version of the course.

#### If there's no "building" up the project, then why include it in the name?

This is also a good question and I hear you. I think I can do a better job of
this in the new version. Thanks to your feedback, this is what I came up with.

Instead of going over the final code base and picking apart each component, I'm
going to include separate branches of the code base and we'll go over building
up the project in stages.

For example, maybe the first section will show setting up a simple Flask app to
serve a static home page. Then the next section will introduce users, and so on.

This will allow you to see the code base at various stages of complexity and will
very likely make everyone happy.

It also means you'll be able to easily pull out various components that you don't
want in your own custom apps because you'll be able to see a `git diff`.

#### A lot of people wanted an API component, so I'm including one

This won't be gigantic but it will definitely cover a lot of material related to
creating a legit public API. You'll be comfortable enough to create your own API
in the end.

#### The course's structure will be greatly improved

The first iteration wasn't too bad. I mean, it was separated pretty well and you
were able to jump around sections by using time-linked shortcuts.

However, like everything else in life. It can be improved upon.

Now I'll really be breaking things up in such a way that you can digest and get
value out of bite sized lectures.

I'm aiming to have more lectures, but less length for each one. This will make
it easier to skim and find topics you're interested in learning about.

#### Dedicated notes for each lecture will be included

Each lecture will contain full blown PDF notes that will reference every single
command ran in the lecture as well as websites or other material mentioned.

The goal here is to give you an excellent reference that you can use later on
after going through the course without having to re-watch the lectures.

I've done this in my other courses and a lot of students love this feature.

#### No more self hosted course platform

Not a single person complained about how the original screencasts were distributed.

It's simple and it works. It also gives you a DRM-free way to follow the screencasts
even if you have no internet connection.

I would consider it a success, given I whipped up the entire solution in about
a week to make sure everything was released on time.

I think it can be better though! So rather than spend months improving it, I'm
simply going to host it on Udemy like I am with my other courses.

This will give you guys a very good course viewing experience, and it also makes
distributing updates much better for both of us.

There will be no more downloading and combining the contents of zip files. You'll
just be able to stream videos and if I push an update, you'll get it instantly.

Another awesome advantage of this is there will be dedicated forums where students
can post questions and answers. We'll build a community together.

#### How much content will there be and how much will it cost?

It's too soon to determine the length of it. It's going to be a very
comprehensive course. I would guess about 6 hours of fast paced video content.

I'm not sure yet on the new price, but one thing is for sure... it's going to be
closer to the price of chinese food instead of the price of a car payment.

#### When will it be released?

It needs to be created from the ground up before it can be released. I plan to
start working on it nearly full time in about 2 weeks.

It's too soon to estimate release dates. I will do my best to get it out in
about 2 months from then but I can't promise anything.

The best I can say is, no less than 2 months but almost certainly no more than 4.

### That's only the tip of the iceberg

I just wanted to share with you a few guaranteed changes that will happen in the
next version of Build a SAAS App with Flask.

There will very likely be new additions as I start planning it all out.

If you're not already a student then I recommend signing up below to get notified
when it's out.

<!-- Begin MailChimp Signup Form -->
<div id="mc_embed_signup" class="margin-top-md">
<form action="//nickjanetakis.us9.list-manage.com/subscribe/post?u=ed476286695fd77da0853a1a3&amp;id=b99ea8a9fb" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">

<div class="mc-field-group">
    <input type="email" placeholder="Enter e-mail address..." value="" name="EMAIL" class="required email" id="mce-EMAIL">
</div>
    <div id="mce-responses" class="clear">
        <div class="response" id="mce-error-response" style="display:none"></div>
        <div class="response" id="mce-success-response" style="display:none"></div>
    </div>
    <div style="position: absolute; left: -5000px;"><input type="text" name="b_ed476286695fd77da0853a1a3_b99ea8a9fb" tabindex="-1" value=""></div>
    <div class="clear"><input type="submit" value="Get notified" name="subscribe" id="mc-embedded-subscribe" class="input inline btn orange"></div>
    </div>
</form>
</div>
<!--End mc_embed_signup-->

<br>

It's going to take you from being a novice with Flask to being comfortable
developing a production grade non-trivial Flask application that accepts
recurring payments and much more.

I'll be including a dedicated course page with all of the details once the course
is ready to be consumed.
