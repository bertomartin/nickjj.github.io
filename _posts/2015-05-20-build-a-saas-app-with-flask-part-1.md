---
layout: post
title: 'Build a SAAS App with Flask: Part 1'
tags: [flask, bsawf, tutorial]
excerpt:
  Learn about the Build a SAAS App with Flask project, this is part 1 of a 5
  part series.
---

---

<div class="center margin-top-md margin-bottom-md">
  <h2>This post is very outdated</h2>
  <a class="btn green" href="{{ site.baseurl }}courses/build-a-saas-app-with-flask">
    Check out version 2 of this course!
  </a>
</div>

---

Today I decided to publish the first version of the source code for the Build
a SAAS App with Flask course. It is the same project that was
<a target="_blank" href="https://www.kickstarter.com/projects/nickjj/build-a-saas-app-with-flask-and-deploy-it-with-doc/description">funded on Kickstarter</a>.

Details can be found on the official repo for the project:  
[http://github.com/nickjj/build-a-saas-app-with-flask](http://github.com/nickjj/build-a-saas-app-with-flask)

#### Looking for the other parts of this series?

- Part 1
- [Part 2]({% post_url 2015-05-23-build-a-saas-app-with-flask-part-2 %})
- [Part 3]({% post_url 2015-05-30-build-a-saas-app-with-flask-part-3 %})
- [Part 4]({% post_url 2015-06-05-build-a-saas-app-with-flask-part-4 %})
- [Part 5]({% post_url 2015-06-24-build-a-saas-app-with-flask-part-5 %})

### Baseline features

- Project structure is in place
- Docker is setup to run both the website and Celery
- CLI app called “run” is setup to help you manage the app
- i18n (translations) for a number of things
- Cache backend is wired up with Redis
- Celery is wired up with Redis
- E-mail is setup to work through Celery
- Custom extension has been written for templated e-mails

### Assets

- Assets are accounted for with a custom extension and webpack
- Asset server is setup for development and compiles SASS instantly
- Font awesome 4.3.0 is ready to rock

### User module

- 100% test coverage
- Users can register themselves
- Users can login
- Users can recover forgotten passwords
- Users can update their login credentials
- Users can optionally create a username after registering
  - Or create one from their settings if they have yet to make one

### Support module
- 100% test coverage
- Visitors can submit issues which get saved to the database

### Billing module

- Pricing table front-end is setup

### Pages module

- Visitors can view the home page
- Visitors can view the FAQ
- Visitors can view the privacy policy
- Visitors can view the terms of service

There may be more features implemented by the time you read this. The github repo
will be the source of truth for features from this point on.

### On the horizon

You can expect a lot more in the near future, such as the billing component and
an admin dashboard among other things.
