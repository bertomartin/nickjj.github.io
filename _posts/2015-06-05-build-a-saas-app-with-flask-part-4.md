---
layout: post
title: 'Build a SAAS App with Flask: Part 4'
tags: [flask, bsawf, tutorial]
excerpt:
  Learn about the Build a SAAS App with Flask project, this is part 4 of a 5
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
- Part 4
- [Part 5]({% post_url 2015-06-24-build-a-saas-app-with-flask-part-5 %})

### What's been added since the third installment?

Real time tweets are streamed over a websocket server. I know part 3 ended off
with better tests coming next, but that didn't seem worthy of a dedicated post.

The good news is there's a lot higher test coverage now and the tests have been
re-worked quite a bit. The important bits of the app have very high test coverage.

![Test coverage]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-test-coverage.jpg "Test coverage")

#### Twitter stream

- Connect to Twitter's streaming API
- Read in tweets as they come in

![Tweet stream]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-twitter-stream.jpg "Tweet stream")

#### Broadcast queue

- Broadcast the stream events through a rate limited task queue

![Broadcast queue]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-broadcast-queue.jpg "Broadcast queue")

#### Paid members can view it in a browser

![Real time stream]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-real-time-stream.jpg "Real time stream")

#### CLI additions

- `run routes` to get a list of all available routes
- `run stream` to listen, broadcast or fake broadcast to the websocket server

### On the horizon

A lot of refactoring to clean up and normalize the code base. Now that we have a
lot of test coverage, this is the perfect time for doing that.
