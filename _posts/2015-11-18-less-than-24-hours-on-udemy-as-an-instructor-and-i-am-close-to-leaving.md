---
layout: post
title: 'Less than 24 Hours on Udemy as an Instructor and I Am Close to Leaving'
tags: [udemy]
excerpt:
  Read a few horror stories about what it's like to be an instructor on Udemy's
  course hosting platform.
---

## Goal of this post

I want to give Udemy some constructive criticism in the open while also warning
potential course creators of the pitfalls I've encountered while using Udemy to
sell a course.

All of the comments below are accurate as of the date of this blog post
(November 18th 2015). Hopefully some of the issues have been fixed since then.

I released a course on Udemy about a day ago and have spent the last few weeks
battling their platform, here's what I've learned from that experience.

**TL;DR** Skim down to the screenshots and start reading from there.

## Short recap of the courses I've created recently

Back in June 2015 I ran my first Kickstarter for the
<a target="_blank" href="https://buildasaaswithflask.com/">Build a SAAS app with Flask</a>
screencast series.

I went ahead and created my own makeshift course hosting platform while also
creating the course itself at the same time, and in the end everything went
pretty well. Things got released and backers were happy.

The makeshift platform I created was definitely rough around the edges and not
as streamlined as it could be for both me the developer and students of the course
but so far I haven't gotten a single complaint about the platform.

In October 2015 I ran a 2nd Kickstarter for
<a href="{{ site.baseurl }}courses/docker-for-devops-from-development-to-production">The Docker for DevOps course</a>
and it got funded as well.

I wanted to try Udemy as a platform this time around because the last thing I
wanted to do was build another platform to distribute the content and I heard a
lot of great things about Udemy from people who have taken courses on it.

## Students seem to really love Udemy

Before I announced the course was going to be hosted on Udemy, I even had a few
backers ask me if it would be on Udemy and they were really happy that in the
end I already had plans to host it there.

During one of Udemy's endless $10 flash sales that instructors can opt-into
being a part of, I even bought a course on Android development simply because
I'm kind of interested in branching out to mobile app development but my main
motivation was to get a feel of Udemy's platform from a student's point of view.

### Their platform is pretty good for students

I have to admit I was impressed. It certainly wasn't a perfect experience but it
was pretty damn good.

I'm not a fan of seeing 15-20 minute lectures without any way to time-jump around
sub-sections of the video -- heck even my video watching page I created in
literally 3 hours had this feature.

But, everything else was pretty good. The table of contents was easy to navigate,
the videos played well at the default size and it was easy to see external
resources that you could download for a lecture and even see discussions on a
specific lecture.

#### Plot twist: alien mouth noises are gross

As a buyer of a $10 course I was pretty happy. The instructor, despite having
tens of thousands of students and great reviews had serious microphone issues
and you could hear spit crackle in between his teeth every time he said a word
but that's hardly Udemy's fault.

It was really disgusting sounding because it was so loud and with headphones on,
it sounded like some guy was hunched over your shoulder just moving spit around
his mouth directly into your ear while breathing heavy.

Don't worry, the point of this post isn't about that, I just wanted to point out
that just because a course has a ton of students doesn't mean it's good. In fact,
I fast forwarded the course at 2x speed the whole way through because the
instructor took 10 minutes to explain concepts that should have been explained
in 2 minutes.

However, I definitely got my $10 in value from it so I'm not complaining.

## Creating a course as an instructor

I reported multiple bugs to the Udemy team, most went unanswered while others
replied back with canned phrases like "we realize that it's a bug" with no sign
of resolution.

We're talking huge bugs like simply wanting to format a text lecture. The HTML
it generates was entirely broken, but it previewed fine, however as soon as you
publish the lecture, the formatting was totally broken.

### Coupon creation system is pure jokes

There's also some hideously bad UI decisions made for instructors. For example,
I had to create 90x 100% off coupons for my Kickstarter backers because part of
backing my Kickstarter was to get the course for free when it was released.

Well, you can only create 1 coupon at a time, and it doesn't even bother trying
to pre-seed a random easy to read coupon code for you. My self baked solution
preset a unique human readable coupon for you automatically and that entire
feature with nearly 100% test coverage took a few hours to implement.

Human readable as in, it avoided using certain letters of the alphabet so people
didn't have to worry about if a letter was a capital I or lowercase l.

#### Backspace is broken

The coupon creation gets way worse, when entering in a final price amount you
can't even hit backspace in the text field. Backspace and delete are simply a
null operation, that's cool.

So you have to close out the annoying create coupon modal form that takes 3
seconds to load and start over if you fat fingered an amount. Thanks for that Udemy.

#### Sorry, fixed price coupons only

Oh, but it gets worse trust me. You can only create fixed amount coupons, not
percent off. So if your course is $100 and you want to sell it for 20% off, you
have to put in $80.

Fine, that's reasonable until you decide you want to change the price of your
course to $70 and now all of those coupons you created for $80 are pointless
since the coupon would increase the price of the course.

Well, just go and delete the old coupons right? Nah, Udemy doesn't let you delete
any coupons. The best you can do is deactivate them one at a time, and then hide
it but this also means you're unable to ever use that coupon code again.

That's a real bummer because it's nice having a code like "BLOG20" to imply 20%
off from someone who reached your course through your blog, but nope. The old
BLOG20 code is going to stay forever and you need to pick another name.

### Fleshing out the course

There's extremely questionable design decisions made here, such as imagine
having 105 lectures in a drag/drop/re-orderable list widget. Imagine that this
entire list is about 15 pages of scrolling down on a 1080p monitor.

Well, the button to create a new lecture is all the way on the bottom. So the
first thing you need to do is scroll down for 10 years until you reach it, then
you click the button and name the lecture.

Now you need to click and drag that lecture slowly up to where you want. This
takes many seconds if the drop point isn't close to the bottom. Typically video
lectures have 2 lectures total, so you need to do this twice.

This is infuriating because you'll have to do this dozens of times to just flesh
out your course. I wish I knew how they tested this stuff because it's certainly
not on instructors.

### Seeing who bought your course

They give you a reasonable way to see who bought your course but you don't get
any e-mail addresses, just the student's Udemy name and how much they paid.

I would really like to see more analytics about purchase breakdowns. Part of
using a platform like this is to have insight on how you're moving your product
but Udemy is lacking big time in this area.

### Lack of ways to backup your course and insecure by default

I think it would take me over a day to assemble my course from scratch due to
all of the UI issues of their platform. I would also certainly forget the order
of everything because there's over 100 lectures.

While you can't delete a course once it has students, you can delete lectures
which is just as bad. So if a disgruntled student manages to social engineer your
password from you or you lose your laptop then you could potentially be in a
world of hurt.

I would like to see a 1 click solution that allows me to back up my course to a
single zip file and then have the option to import it. This way if something
terrible happens, I can recover in however long it takes me to upload a few gigs
of video.

I would also like to see 2 factor authentication added.

### Terrible UI performance on the back-end

The course's main back-end dashboard takes 10 seconds, 85 web requests and needs
to serve 4.5MB of Javascript and CSS **just to get to the point where you can do
anything**. It looks like a mixture of Angular and jQuery.

**Take a peek at the development tools (bottom right) if you don't believe me:**

![Worst Udemy UI performance]({{ site.baseurl}}assets/img/blog/udemy-is-pretty-bad-for-intructors-poor-backend-performance.jpg)

Those numbers are fully loading the page and hitting the reload button on FireFox
and then taking a screenshot as soon as it's usable.

It also runs horrendously slow once it's all loaded. This is on a quad core i5
3.2ghz with 16 gigs of RAM, an SSD and a 30Mb internet connection. Unfortunately
this will be the page you end up loading the most because it's the gateway to
everything important.

Most of the other back-end pages are pretty poor too, a lot of pages take 4-5
seconds to load with dozens and dozens of requests with megabytes of assets.

It makes using the overall platform feel really poor. I can't imagine how bad it
must be for someone on a low end machine.

### Udemy brands your intellectual property with their logo

It's a reasonable idea to watermark all of your videos with your course's website
URL or perhaps your name so that if your video gets pirated at least there's a
chance someone will find you via the watermark.

With Udemy you're sort of out of luck here. They will brand every single video
you upload with their logo in the bottom right with no way out opt-out of this.
The bottom right is the most ideal place for placing a watermark.

This is extremely misleading because they are branding your videos, but they
have absolutely nothing to do with creating the content. The content is yours,
not theirs.

It also means now you need to litter your videos with multiple watermarks which
in the end just hurts students because it's distracting.

As of November 18th 2015 there is no mention of this in their terms of service,
so they are doing this without your consent.

### Udemy blacklists you from their platform unless your course is on sale for $10 nearly all the time

Well, now it's time to get into the thing that really pushes me over the edge.
I can deal with all of the above but this part kills me inside.

I signed up with Udemy to reach millions of students. Udemy runs $10 course deals
pretty much every week and they last for days or more.

They are even running this crazy deal right now that lasts for about 10 days.
It's the "Black Friday Blowout".

If you don't opt-into selling your course for $10 then it becomes nearly
impossible for students to find your course.

**Take a look at this screenshot, it was after going to udemy.com while logged
out and then searching for "Docker":**

![Udemy course page with sales]({{ site.baseurl}}assets/img/blog/udemy-is-pretty-bad-for-instructors-courses-on-sale.jpg)

Notice how my course isn't in the list and that the search automatically only
shows courses that are tied into that promotion. You as a user of the platform
would have to manually uncheck that to even see courses not opted into the promotion.

It's actually false advertising because they label it as "sale", which is untrue.
My course is on sale, it just happens to not be on sale for $10 through Udemy.

**Now if you look at the list below, you can see my course on the bottom but it's
also not tagged as being on sale as part of their promotion:**

![Udemy course page all sales]({{ site.baseurl}}assets/img/blog/udemy-is-pretty-bad-for-instructors-courses-all.jpg)

Imagine if you're new to Docker and you see a couple of courses for 10 bucks and
this other course for $149 (which btw you can get for 20% off by going to
  [dockerfordevops.com](http://dockerfordevops.com)).

The worst part about it is they rank by popularity too and it's fairly obvious
that a course on sale for $10 is going to sell more than a course that's hidden
from their UI by default and potentially be 10x the price so you have no chance
to ever rank well in search.

It gets way worse in bigger niches where there's multiple pages of courses, no
one will ever be able to find you then.

I feel like Docker isn't a big enough niche to spam sell the course for $10 because
Udemy will keep 50% of all sales that didn't originate from your own direct links.
So basically I walk away with $5 (~3% of the course's listing price) for a full
blown course that took months to make and years of experience to eventually create.

I'm not a greedy person but I refuse to sell my course for $5. The highest
selling Docker course right now on Udemy has 800 students and I would bet 95% of
his sales were for $10 which means this guy probably has seen about $4,000.

$4,000 can go a long ways but you can also work at McDonalds for about 2 months
and make the same amount. I'm sure the guy running that Docker course has had it
up for more than 2 months too.

### At the end of the day Udemy only cares about sales and students

This is a fair assessment to make given the above. Udemy has millions of students
and tens of thousands of courses.

All they have to do is spam $10 sales all year round (which is what they do) and
get tens of thousands of students to make $10 purchases. Udemy students are
trained to only ever buy courses for $10.

If you aggregate all of that together you can see Udemy is crushing it. The
problem is, instructors are getting completely crushed from these $10 sales.

Combine that with their 30 day refund policy (which is fine btw), you as a
student can even buy the course for full price, and then 2 weeks later if they
release a $10 promo deal you can just refund the course and buy it for $10.

Essentially every course on their platform is $10 or blacklisted.

Now, one thing that's really nice about Udemy is. You can self promote your
course and keep about 97% of the revenue as long as you promote your course with
a coupon and the sale didn't originate from udemy.com.

That means I can give students a 20% off coupon. If the course costs $149, then
it's $119 with the coupon, of which I'll see $115ish. I'm super happy with that,
but the problem is Udemy makes it almost impossible to do this.

**Check out the screenshot below, this is the result of directly linking someone
to my course with a 20% off coupon:**

![Docker for DevOps course page]({{ site.baseurl}}assets/img/blog/udemy-is-pretty-bad-for-instructors-docker-for-devops-course-page.jpg)

They do everything in their power to convince students not to buy your course by
surrounding your course with distractions about their $10 promotions. They even
modify the background image of your course without your consent to further notify
users that a sale is happening as they scroll down.

If I send a potential student to this link, the first thing he'll probably do is
leave my course and find one for $10. So much for self promotion eh?

#### Percent based promo system is misleading

They have another promo system that you can opt-into where they promote your
course for about 25-75% off. The problem is, it's not a promotion.

They permanently offer these % based coupons year round and it's not really
something they promote. It's just coupon codes floating around on the internet.

That's super shady because their TOS explicitly says "You agree that We may offer
Your Course(s) in limited time deals and price tests for a discount of up to and
including 75% off the Base Price.".

Sure, it's limited time in the sense that every month they recycle new 75% off
coupon codes so technically they adhere to their TOS but what it really means is
your course is 75% off year round.

I just had a student buy the course for 75% off and I saw the coupon code that he
used. I never received a Udemy e-mail about the promotion, which is what they
constantly send out for the $10 deals.

It was a general 75% off coupon created back in April 2015 (7 months old). I asked
support and they told me the coupon was set to expire in 2016 and that there are
many coupons like this.

They refused to give me a list of coupon start/end dates when I politely asked
but mentioned a small percent of them run for much longer durations.

So if you opt into percent based promos when you create your course, you are
giving Udemy free reign to sell your course for 75% off indefinitely.

Combine this with the constant $10ish deals which auto-hide your course if you're
not opt-in then it's safe to say Udemy is going to do very little to help you
sell your course.

#### Affiliate market is even worse

It's common for affiliates to take a 20-35% commission anywhere else but on
Udemy's platform that's not the case. You only walk away with 12.5% of the
course's price. Udemy and your affiliate member eat up 87.5% of the revenue.

A book publisher will happily give you better margins than that AND print you
high quality hard cover books while bending the world to sell it for you in the
process. It makes no sense at all.

Here let me break it down for you:

- You put your course up at $149
- Affiliate sales are 50% of your asking price for the buyer (out of your control),
so in this case someone bought the course for $75 through an affiliate link
- The affiliate link owner receives $37.50
- Udemy receives $18.75
- You receive $18.75

Totally insane right? What kind of backwards system is that. Why on earth would
I ever agree to something as inconceivable as that?

Udemy is a really shady company too because you can opt into or out of the
affiliate system but the terms of service for this agreement is not like the fixed
and percent promo TOS.

It only mentions agreeing to the service, not giving an option like the others
to opt in or out of the service. It very much reads like you have to agree just
to use their platform.

It also doesn't help that they don't send you e-mail notifications for affiliate
sales, so it's very easy to not even notice you're selling your course for
basically 88% off.

## Someone needs to step up and end this

Udemy wasn't always like this. A few years ago when they were struggling for
students the margins were much better for instructors.

It wasn't until they've gotten more students that they started pushing the limits
to just how bad they can rip instructors off.

They basically have a platform that prints money and even encourages low quality
courses because their goal is to push $10 courses and pocket $5. A cheap course
for the student has the lowest chances of a refund, and the highest chance of
selling.

That is the perfect formula to brainwash students into only buying $10 courses.

### So, what does this mean for me?

I'll continue to use Udemy for this course until something better comes along,
mainly due to my Kickstarter obligations but I will never in a million years
consider using them in the future.

Hopefully they also reconsider their business model because without instructors,
then students are going to leave. Speaking of which, do you guys know of any
other course hosting platforms?

Right now it only makes sense to use Udemy if you target a huge niche like mobile
app development and can afford to sell your course for $5 profit and expect to
get tens of thousands of students. Otherwise you're better off working at
McDonalds or opening up a lemonade stand.

I'm not someone who typically rants about things, but this experience rubbed me
in such a bad way that I wasted an entire hour to post this because I feel like
the topic is worth writing about.

Thanks for reading!
