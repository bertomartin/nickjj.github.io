---
layout: post
title: 'Build a SAAS App with Flask: Part 2'
tags: [flask, bsawf, tutorial]
excerpt:
  Learn about the Build a SAAS App with Flask project, this is part 2 of a 5
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
- Part 2
- [Part 3]({% post_url 2015-05-30-build-a-saas-app-with-flask-part-3 %})
- [Part 4]({% post_url 2015-06-05-build-a-saas-app-with-flask-part-4 %})
- [Part 5]({% post_url 2015-06-24-build-a-saas-app-with-flask-part-5 %})

### What's been added since the initial release?

The main addition is an admin section. In its initial form, it has the following:

- A dashboard page for a high level overview of everything
- Manage users and issues
- Search, sort, pagination and bulk delete features

![Dashboard]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-admin-dashboard.jpg "Admin dashboard")

### You might be wondering, why not use Flask-Admin?

That's a good question. Having worked on a lot of projects, I never once ended
up being able to use a generic admin backend solution and felt good about it.

They tend to be great if you're dealing with very ordinary data sets and don't
care about creating a good user experience for the person viewing the admin.

#### Different resources tend to have different needs

I don't know about you but if I'm editing a blog post or editing a user account
I would expect to see completely different views.

The blog post view might contain a large typing area, a split panel for real
time previews and various other components that make writing a better experience.

On the other hand, when looking at a user's account I would expect to see a bunch
of details such as their last login time, their account status and billing history.

![Edit user]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-admin-user-details.jpg "Edit user")

#### Generic solutions are usually tedious to customize

No one knows your code better than you. Personally I'm a fan of slightly more
code in favor of avoiding leaky abstractions.

Not only that but I don't like to pigeon hole myself into technical choices. For
instance as an app grows it may become a reasonable idea to introduce something
like Elasticsearch for more sophisticated data analysis.

I want to be able to implement Elasticsearch and wire in faceted navigation to
my existing admin as painlessly as possible. A generic solution is not going to
allow you to do this, or if it does you're going to end up writing a lot of
crazy code.

### What does the default admin panel look like?

![Manage issues]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-manage-issues.jpg "Manage issues")

![Bulk delete]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-bulk-delete-items.jpg "Bulk delete items")

In case you're wondering, the e-mail addresses above were generated using the
[Faker package](https://github.com/joke2k/faker). Sorry in advance if anyone is
on that list.

Oh yeah, you're probably wondering why the date format is so ugly. I haven't
setup momentjs yet. It will be adjusted in a future version.

### On the horizon

The next step is adding all of the billing and subscription components to the app.
