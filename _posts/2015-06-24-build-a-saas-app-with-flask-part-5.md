---
layout: post
title: 'Build a SAAS App with Flask: Part 5'
tags: [flask, bsawf, tutorial]
excerpt:
  Learn about the Build a SAAS App with Flask project, this is part 5 of a 5
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

The source code can be found here:  
[http://github.com/nickjj/build-a-saas-app-with-flask](http://github.com/nickjj/build-a-saas-app-with-flask)

#### Looking for the other parts of this series?

- [Part 1]({% post_url 2015-05-20-build-a-saas-app-with-flask-part-1 %})
- [Part 2]({% post_url 2015-05-23-build-a-saas-app-with-flask-part-2 %})
- [Part 3]({% post_url 2015-05-30-build-a-saas-app-with-flask-part-3 %})
- [Part 4]({% post_url 2015-06-05-build-a-saas-app-with-flask-part-4 %})
- Part 5

### Highlights from this version

- Change the theme to Bootstrap
- Add i18n support along with a Spanish translation
- Add new functionality to the `run db` commands
- Use timezone aware UTC dates on the Python side
- Use momentjs to handle all date formatting
- Fix going to the “next” url after login
- Drastically enhance the webpack set up
- Add custom error pages
- Major refactor of the entire code base
- Adapt MIT license to the code base

### Other changes

- Update forms to process all HTTP verbs
- Use JSON as a Celery serializer
- Fix missing admin seed account when running `run add users`
- Add example settings.py file for production use
- Add Google Analytics snippet
- Add robots.txt and public favicons
- Fix not cancelling subscriptions when deleting users
- Upgrade multiple package dependencies
- Upgrade Postgres and Redis versions

You can view the entire commit history since the last build here:  
[https://github.com/nickjj/build-a-saas-app-with-flask/compare/v0.0.2…v0.1.0](https://github.com/nickjj/build-a-saas-app-with-flask/compare/v0.0.2...v0.1.0)

### Screenshot gallery

![Admin dashboard]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-new-admin-dashboard.jpg "Admin dashboard")

View all 11 screenshots here:
<a target="_blank" href="http://imgur.com/a/M6dbH">http://imgur.com/a/M6dbH</a>.

### On the horizon

I will let this version simmer for a bit while working out the details for the
screencast series. Once the build is solid it will be feature frozen and placed
into a branch that the screencasts will be based on.

Development on the project will still happen after the casts are made.
