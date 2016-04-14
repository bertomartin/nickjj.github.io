---
layout: post
title: 'Alpine based Docker images make a difference in real world apps'
tags: [docker]
excerpt:
  We all know that Alpine based Docker images are smaller, but how much does it
  matter for non-trivial applications that need libraries compiled?
---

I develop a lot of Python and Ruby based applications, and my `Dockerfile`
typically pulls in from the official Python or Ruby images on the Docker Hub.

Up until recently, you only had 3 choices as a base OS. You could choose to use
Jessie, Wheezy or Slim. However, now you can also choose Alpine as a base.

I imagine most people used the slim variant, and then installed things like
`build-essential` in their `Dockerfile` if they needed it to compile libraries
that their app's packages use.

Today I tried out Alpine and here's the results.

### What's considered a real world application?

I'm currently in the middle of creating a new demo application for the
[Build a SAAS App With Flask]({% post_url 2016-03-14-build-a-saas-app-with-flask-is-getting-a-complete-make-over-soon %})
course that I'm remaking.

It currently has around 30 top level Python packages and thousands of lines of
code. It is a real application that connects to multiple databases and a few
package dependencies require libraries to be compiled to function.

I'm a huge backer of Docker, not in a financial sense but I truly believe it's
a great tool so naturally I'm going to be using Docker in the course.

### How does Alpine compare to Debian Jessie (Slim)?

`python:2.7-slim` as a base for my `Dockerfile` produces a **467.4MB** image.
`python:2.7-alpine` as a base for my `Dockerfile` produces a **309.1MB** image.

That's a huge win. The **final image is ~33% smaller** and all I did was switch
the base image and then spent 5 minutes learning how to use Alpine's package
manager.

### `Dockerfile` comparison

##### The Slim version

```sh
FROM python:2.7-slim
MAINTAINER Nick Janetakis <nick.janetakis@gmail.com>

RUN apt-get update && apt-get install -qq -y \
  build-essential libpq-dev libffi-dev --no-install-recommends

ENV INSTALL_PATH /bsawf
RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

CMD gunicorn -b 0.0.0.0:8000 --access-logfile - "bsawf.app:create()"
```

##### The Alpine version

```sh
FROM python:2.7-alpine
MAINTAINER Nick Janetakis <nick.janetakis@gmail.com>

RUN apk update && apk add build-base postgresql-dev libffi-dev

ENV INSTALL_PATH /bsawf
RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

CMD gunicorn -b 0.0.0.0:8000 --access-logfile - "bsawf.app:create()"
```

In this case, I need `libffi-dev` to compile a bcrypt package dependency and
`libpq-dev` is for postgresql.

The Alpine image also has some room to improve because I'm pretty sure the
`postgresql-dev` package is pulling in a lot more than `libpq-dev` on Debian.

### Room to improve?

Probably. I didn't bother hunting down the specific dependencies needed to
compile the postgresql and bcrypt related libraries.

Using `build-essential` and `build-base` is a safe bet because they include
pretty much everything you'd need to compile most packages.

Overall I'd say using an Alpine based image is well worth it. It doesn't take
long to track down the `apk` version of popular `apt` packages and the savings
is huge.
