---
layout: post
title: 'Alpine Based Docker Images Make a Difference in Real World Apps'
tags: [docker]
excerpt:
  We all know that Alpine based Docker images are smaller, but how much does it
  matter for non-trivial applications that need libraries compiled?
---

I develop a lot of Python and Ruby based applications, and my `Dockerfile`
typically pulls in from the official Python or Ruby images on the Docker Hub.

Up until recently, you only had 3 choices as a base OS. You could choose to use
Jessie, Wheezy or Slim. However, now you can also choose Alpine as a base.

I imagine most people used the Slim variant, and then installed things like
`build-essential` in their `Dockerfile` if they needed it to compile libraries
that their app's packages use.

In this post you're going to see how Alpine compares to Debian Jessie (Slim)
and also learn how to optimize the Alpine version even more.

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

That's only the beginning too because **we can shrink it down by an additional
~260%** by introducing a few tricks into our `Dockerfile`.

### Phase 1 Dockerfile comparison

Phase 1 is a direct comparison of Debian Jessie (Slim) vs Alpine with no
additional tricks to minimize the final image size.

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

### Phase 2 Alpine based Dockerfile

At the moment, the Alpine version is 33% smaller but what happens when someone
with more knowledge on Alpine than myself looks at it for a few minutes?

That's what happened today when 
<a target="_blank" href="https://twitter.com/n_copa/status/720954662954905600">@n_copa reached out to me on Twitter</a>
and gisted a new version of the `Dockerfile`.

```sh
FROM python:2.7-alpine
MAINTAINER Nick Janetakis <nick.janetakis@gmail.com>

ENV INSTALL_PATH /bsawf
RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

COPY requirements.txt requirements.txt
RUN apk add --no-cache --virtual .build-deps \
  build-base postgresql-dev libffi-dev \
    && pip install -r requirements.txt \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
                | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                | sort -u \
                | xargs -r apk info --installed \
                | sort -u \
    )" \
    && apk add --virtual .rundeps $runDeps \
    && apk del .build-deps

COPY . .

CMD gunicorn -b 0.0.0.0:8000 --access-logfile - "bsawf.app:create()"
```

The above `Dockerfile` dropped the final image size from **309.1MB** to
**117.3MB**.

That's **~260%** smaller than the original Alpine image. It's not fair to compare
it against the Debian Jessie (Slim) version because we're not cleaning up our
compile-time dependencies, but it's **~400%** smaller as is.

#### What's the catch?

The biggest downside is every time you change a package in your application, it
will have to run through the entire `apk add` command which means all of the
system dependencies will be re-installed.

This is going to add a few minutes to your build times, but remember -- this
increase only happens when you change your app's package dependencies.

For typical code changes which is what 99% of your changes will be, the build
time will be nearly identical with both versions.

### Is Alpine worth it?

Is it worth the occasional build time increases to ship around a 117MB image
instead of one that's over 300MB? That's for you to decide, but I think it is.

I'm really happy with Alpine, and you can expect the official Docker Hub
versions of many images to support it in the near future.

For example,
<a target="_blank" href="https://hub.docker.com/_/redis/">Redis already has an
Alpine version</a> and it's only **~16MB**.
