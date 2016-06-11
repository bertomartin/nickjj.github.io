---
layout: post
title: 'Dockerize a Flask, Celery, and Redis Application with Docker Compose'
tags: [flask, docker, tutorial]
excerpt:
  Learn how to install and use Docker to run a multi-service Flask, Celery and
  Redis application in development with Docker Compose.
---

After this tutorial, you'll understand what the benefits of using Docker are
and will be able to:

- Install Docker on all major platforms in 5 minutes or less
- Clone and run an example Flask app that uses Celery and Redis
- Know how to write a Dockerfile
- Know how to run multiple Docker containers manually
- Run multiple Docker containers with Docker Compose

## What is Docker and why is it useful?

[Docker](https://www.docker.com/){:target="_blank"} allows you to package up an
application or service with all of its dependencies into a standardized unit.
This unit is typically labeled as a Docker image.

Everything the application needs to run is included. The Docker image contains
the code, runtime, system libraries and anything else you would install on a
server to make it run if you weren't using Docker.

To get a better idea of how Docker will affect you on a day to day basis as a
software developer I highly recommend you read one of my previous blog posts
which will 
[save you from years of turmoil by using Docker]({% post_url 2016-05-02-save-yourself-from-years-of-turmoil-by-using-docker-today %}){:target="_blank"}.

## Installing Docker

The code base we'll be working with was created against Docker v1.11 so I
recommend that you install the latest v1.11 release.

We'll also be using Docker Compose v1.7.

You could always upgrade to something newer on your own after the tutorial.

### OSX

<iframe width="720" height="405" src="https://www.youtube.com/embed/lNkVxDSRo7M?rel=0&iv_load_policy=3" frameborder="0"></iframe>

- [Download the latest v1.11 release from GitHub instead of following his steps](https://github.com/docker/toolbox/releases){:target="_blank"}

### Windows

<iframe width="720" height="405" src="https://www.youtube.com/embed/S7NVloq0EBc?rel=0&iv_load_policy=3" frameborder="0"></iframe>

- [Download the latest v1.11 release from GitHub instead of following his steps](https://github.com/docker/toolbox/releases){:target="_blank"}
- Make sure Docker Compose, VirtualBox and Git are checked during installation

### Linux

#### Ubuntu (copy / paste this into a terminal)

```sh
sudo apt-get update -y \
  && sudo apt-get install -y curl apt-transport-https ca-certificates aufs-tools \
  && sudo apt-key adv \
  --keyserver hkp://p80.pool.sks-keyservers.net:80 \
  --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
  && echo "deb https://apt.dockerproject.org/repo ubuntu-$(lsb_release -cs) main" | \
  sudo tee /etc/apt/sources.list.d/docker.list \
  && sudo apt-get update -y \
  && sudo apt-get install -y docker-engine=1.11.2-0~"$(lsb_release -cs)" \
  && sudo usermod -aG docker $(whoami)
```

- Make sure to completely logout of your OS before continuing

#### Other distros

[https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/){:target="_blank"}

#### Installing Docker Compose v1.7.1 (copy / paste this into a terminal)

```sh
curl -L https://github.com/docker/compose/releases/download/1.7.1/docker-compose-Linux-x86_64 > \
  /tmp/docker-compose && \
  chmod +x /tmp/docker-compose &&
  sudo mv /tmp/docker-compose /usr/local/bin
```

### Check and make sure Docker and Docker Compose are working

You should see what I see, or something very similar:

```sh
docker --version
> Docker version 1.11.2, build b9f10c9

docker-compose --version
> docker-compose version 1.7.1, build 0a9ab35
```

## Cloning the Flask application

We're going to be using the open source version of the application in my
[Build a SAAS App with Flask course]({{ site.baseurl }}courses/build-a-saas-app-with-flask).

The open source version only covers a tiny fraction of what the course covers,
but it will be more than enough to exercise how to use Docker in development.

### Are you interested in becoming a Flask master?

*Build up a 4,000+ line software as a service application with Flask in stages
where I'll be at your side explaining my thought process every step of the way.*

<a class="btn green" href="{{ site.baseurl }}courses/build-a-saas-app-with-flask">
  Become a Flask Master
</a>

### Clone the project

```sh
git clone https://github.com/nickjj/build-a-saas-app-with-flask
```

- If you don't have git, [you can download it directly](https://github.com/nickjj/build-a-saas-app-with-flask/archive/master.zip).

### Open the project in your favorite code editor

```sh
# Move into the project's directory
cd build-a-saas-app-with-flask

# Open the project with your favorite editor (mine is Sublime)
subl .
```

Feel free to use whatever editor you want, but if you like Sublime Text 3 and
you want to configure it for Python, Docker and more then check out my post on
[25 Sublime Text 3 Packages for Polyglot Programmers]({% post_url 2016-04-13-25-sublime-text-3-packages-for-polyglot-programmers %}){:target="_blank"}.

## Dockerize the Flask application

There's a few things we need to do to Dockerize the application.

### Logging

In order for logs to function properly, Docker expects your application or
process to log to STDOUT. Lucky for us, Flask does this by default.

### Docker specific files

The root of the project has a few files that are related to Docker:

```sh
nick@oriath:/tmp/bsawf (master) ⚡ ls -la
-rwxrwxr-x  1 nick nick    643 Jun 10 12:57 docker-compose.yml
-rwxrwxr-x  1 nick nick    346 Jun 10 12:57 Dockerfile
-rw-rw-r--  1 nick nick     19 Jun 10 12:57 .dockerignore
-rwxrwxr-x  1 nick nick     31 Jun 10 12:57 .env
```

The only file that's necessary to add is the `Dockerfile` but you'll find that
most web applications that are Docker-enabled will have the others.

#### Dockerfile

Let's start off with the `Dockerfile` because to talk about the other files
will require having a little bit of knowledge about how Docker images get built.

You can think of this file as your Docker image blueprint or recipe. When you run
the `docker build` command it will execute each line from top to bottom.

It's going to run all of these commands in the context of the Docker image. So,
just to skip ahead for a second, look at the line below:

`RUN mkdir -p $INSTALL_PATH`

This command is not going to be executed on your workstation. Instead, that
folder is going to be created inside of the Docker image.

At the end of the day, when you build this Dockerfile, it's going to create
a Docker image that has a Debian Jessie base, all of the Flask code and by
default it will run the gunicorn app server.

Let's break down what each line is doing:

```sh
FROM python:2.7-slim
# Docker images can start off with nothing, but it's extremely
# common to pull in from a base image. In our case we're pulling
# in from the slim version of the official Python 2.7 image.
#
# Details about this image can be found here:
# https://hub.docker.com/_/python/
#
# Slim is pulling in from the official Debian Jessie image.
#
# You can tell it's using Debian Jessie by clicking the
# Dockerfile link next to the 2.7-slim bullet on the Docker hub.
#
# The Docker hub is the standard place for you to find official
# Docker images. Think of it like GitHub but for Docker images.
#
# The Flask application you cloned is compatible with Python 3.5
# so if you wanted to use 3.5 instead, you could replace 2.7.


MAINTAINER Nick Janetakis <nick.janetakis@gmail.com>
# It is good practice to set a maintainer for all of your Docker
# images. It's not necessary but it's a good habit.


ENV INSTALL_PATH /snakeeyes
# The name of the application we're building is called Snake Eyes
# and while there is no standard on where your project should
# live inside of the Docker image, I like to put it in the root
# of the image and name it after the project.
#
# We don't even need to set the INSTALL_PATH variable, but I like
# to do it because we're going to be referencing it in a few spots
# later on in the Dockerfile.
#
# The variable could be named anything you want.


RUN mkdir -p $INSTALL_PATH
# This just creates the folder in the Docker image at the
# install path we defined above.


WORKDIR $INSTALL_PATH
# We're going to be executing a number of commands below, and
# having to CD into the /snakeeyes folder every time would be
# lame, so instead we can set the WORKDIR to be /snakeeyes.
#
# By doing this, Docker will be smart enough to execute all
# future commands from within this directory.


COPY requirements.txt requirements.txt
# This is going to copy in the requirements.txt file from our
# work station at a path relative to the Dockerfile to the
# /snakeeyes/requirements.txt path inside of the Docker image.
#
# It copies it to /snakeeyes because of the WORKDIR being set.
#
# We copy in our requirements.txt file before the main app
# because Docker is smart enough to cache "layers" when you build
# a Docker image.
#
# You see, each command we have in the Dockerfile is going to be
# ran and then saved as a separate layer. Docker is smart enough
# to only re-build pieces that change, in order from top to bottom.
#
# This is an advanced concept but it means that we'll be able to
# cache all of our pip packages so that if we make an application
# code change, it won't re-run pip install unless a package changed.


RUN pip install -r requirements.txt
# Like most Flask applications, we have a requirements.txt file
# to define all of our dependencies. So we install them as usual.
#
# We don't need to use virtualenv because our application is
# completely encapsulated in the Docker image. I know, it's awesome.


COPY . .
# This might look a bit alien but it's copying in everything from
# the current directory relative to the Dockerfile, over to the
# /snakeyes folder inside of the Docker image.
#
# We can get away with using the . for the second argument because
# this is how the unix command cp (copy) works. It stands for the
# current directory.


RUN pip install --editable .
# The Flask application has a Click based CLI component to it and
# this command will generate a standard egg-info folder.
#
# This has nothing to do with Docker, but we need to add it here
# to ensure our Docker image is ready to run our CLI commands.


CMD gunicorn -b 0.0.0.0:8000 --access-logfile - "snakeeyes.app:create_app()"
# This is the command that's going to get ran by default if we run
# the Docker image without any arguments.
#
# In our case, it'll start up gunicorn on port 8000. In case you're
# new to Flask, the --access-log - means it will log all output to
# STDOUT. If you remember from before, that's important.
```

At this point we could build the image and you'd be able to access the Flask app,
but let's avoid doing that for now.

#### .dockerignore

Let's first look at the next file which is the `.dockerignore` file.

```sh
.git
.dockerignore
```

When we copied in all of the files from our current directory into the Docker
image with the `COPY . .` command, it's going to copy literally everything.

That's not the best idea in the world because if your project is a git repo
you're going to have a TON of extra data. You should strive to have the smallest
Docker images you can within reason.

The `.dockerignore` file is very similar to a `.gitignore` file. It lets you
black list certain folders or files from being included.

In our case, we're ignoring the git folder but we're also excluding the
`.dockerignore` file itself because it's not part of our Flask application.

#### docker-compose.yml

Docker Compose is an official tool supplied by Docker. At its core, it's a
utility that lets you "compose" Docker commands.

Before you can appreciate just how useful this tool is, we need to go over what
life would be like without Docker Compose.

Let's say say you wanted to get your work station to the point where you could
run the Flask application. You would have to type all of these commands:

```sh
# [Terminal tab 1]
#
# Create a default network to allow Docker containers
# to talk to each other.
docker network create snakeeyes_default

# Pull down Redis from the Docker hub.
docker pull redis:3.0-alpine

# Build the snakeeyes image for the website.
docker build -t snakeeyes_website .

# Run the Redis image that:
# 1. Has a Docker container name of snakeeyes_redis.
# 2. Has a named volume to persist its data.
# 3. Is a part of the snakeeyes_default network.
# 4. Overrides the Redis CMD to run Redis with a password.
docker run --name snakeeyes_redis -v redis:/var/lib/redis/data \
   --net snakeeyes_default \
   redis:3.0-alpine redis-server --requirepass devpassword

# [Terminal tab 2]
#
# Run the Flask application that:
# 1. Has a Docker container name of snakeeyes_website.
# 2. Passes in the PYTHONUNBUFFERED environment variable to fix
#    log streaming so that STDOUT gets piped back to your terminal.
# 3. Volume mounts in the current working directory to
#    /snakeeyes inside of the container, which will override what
#    was built in the Docker image.
#    This is a key concept that will let you actively develop your
#    application without having to re-build your Docker image
#    on each change.
# 4. Map port 8000 on your work station to port 8000 inside the
#    Docker container.
# 5. Is a part of the snakeeyes_default network.
# 6. Overrides the Flask app's CMD to run gunicorn with
#    an extra --reload flag in development so it picks up code
#    changes without having to reload the process.
docker run --name snakeeyes_website -e PYTHONUNBUFFERED=true \
  -v $PWD:/snakeeyes -p 8000:8000 --net snakeeyes_default snakeeyes_website \
  gunicorn -b 0.0.0.0:8000 --access-logfile - --reload "snakeeyes.app:create_app()"

# [Terminal tab 3]
#
# Run the Celery process that does basically everything above except:
# 1. Has a Docker container name of snakeeyes_celery.
# 2. Does not expose any ports.
# 3. Is a part of the snakeeyes_default network.
# 4. Overrides the Flask app's CMD to run celery.
docker run --name snakeeyes_celery -e PYTHONUNBUFFERED=true \
  -v $PWD:/snakeeyes --net snakeeyes_default snakeeyes_website \
  celery worker -l info -A snakeeyes.blueprints.contact.tasks
```

Now, imagine doing that every single time you wanted to start working on your
project because you'd be shutting them down when you're done with each session.

I don't know about you but I'm an optimistic guy and value life highly but if
I had to do that constantly I'd visit the nearest marina, tie an anchor to my
ankles and swim with the fishes.

Lucky for us, Docker Compose exists so no one has to drown to death. You could
even say Docker Compose saves lives.

Here's what life is like with Docker Compose: `docker-compose up --build`.

Now let's take a glance at the `docker-compose.yml` file:

```yaml
version: '2'

services:
  redis:
    image: 'redis:3.0-alpine'
    command: redis-server --requirepass devpassword
    volumes:
      - 'redis:/var/lib/redis/data'
    ports:
      - '6379:6379'

  website:
    build: .
    command: >
      gunicorn -b 0.0.0.0:8000
        --access-logfile -
        --reload
        "snakeeyes.app:create_app()"
    environment:
      PYTHONUNBUFFERED: 'true'
    volumes:
      - '.:/snakeeyes'
    ports:
      - '8000:8000'

  celery:
    build: .
    command: celery worker -l info -A snakeeyes.blueprints.contact.tasks
    volumes:
      - '.:/snakeeyes'

volumes:
  redis:
```

We're using `version: 2` because as of Docker Compose 1.6+, Docker Compose
introduced a new syntax that is going to be used moving forward.

Then we have a `services` namespace that lets us define our services. They are
the same services we ran manually.

As you can see, the properties we define match up with the command line flags
that we passed in to various Docker commands that we ran manually.

Lastly, we have a `volumes` namespace for our named volume(s).

#### .env

This file isn't technically part of Docker, but it's used by Docker Compose.

By default Docker Compose will look for an `.env` file in the same directory
as your `docker-compose.yml` file.

We can set various environment files here, and you can even add your custom
environment variables here too if your application uses ENV variables.

```sh
COMPOSE_PROJECT_NAME=snakeeyes
```

By setting the `COMPOSE_PROJECT_NAME` to `snakeeyes`, Docker Compose will
automatically prefix our Docker images, containers, volumes and networks with
`snakeeyes`.

## Run the Flask application

You can run everything by typing: `docker-compose up --build`. Docker Compose
has many different sub-commands and flags. You'll definitely want to check them
out on your own.

After the `up` command finishes, open up a new terminal tab and check out what
was created on your behalf.

#### Docker images

Run `docker images`:

```sh
snakeeyes_celery     latest              ...         229.1 MB
snakeeyes_website    latest              ...         229.1 MB
redis                3.0-alpine          ...         13.27 MB
python               2.7-slim            ...         184 MB
```

Docker Compose automatically pulled down Redis and Python for you, and then
build the website and celery images for you.

#### Docker containers

Run `docker-compose ps`:

```sh
Name                        State   Ports          
----------------------------------------------------------
snakeeyes_celery_1    ...   Up                             
snakeeyes_redis_1     ...   Up      0.0.0.0:6379->6379/tcp 
snakeeyes_website_1   ...   Up      0.0.0.0:8000->8000/tcp 
```

Docker Compose automatically named the containers for you, and it appended a
`_1` because it's running 1 instance of the Docker image.

Docker Compose supports scaling but that goes beyond the scope of this tutorial.

We can also see which ports the services are using.

#### Docker volumes

Run `docker volume ls`:

```sh
DRIVER              VOLUME NAME
local               snakeeyes_redis
```

Docker Compose automatically created the named volume for Redis. I recommend
you run `docker volume --help` to see what else you can do on your own.

#### Docker networks

Run `docker network ls`:

```sh
NETWORK ID          NAME                 DRIVER
...                 bridge               bridge
...                 host                 host
...                 none                 null
...                 snakeeyes_default    bridge
```

Docker Compose automatically created the network for you. I recommend you
run `docker network --help` to see what else you can do on your own.

### Viewing the site

If you installed Docker through the Docker Toolbox then you'll need to make 1
change to the `config/settings.py` file.

Check out the `SERVER_NAME = 'localhost:8000'` value.

You will need to change `localhost` to your Docker Machine IP address instead.

Chances are that will be `192.168.99.100` but if it's not, you can find your
Docker Machine IP by running `docker-machine ip`.

Then you can check it out in your browser by going to `http://localhost:8000`.
Again, as a reminder, if you're using Docker Toolbox then access your Docker
Machine IP address instead.

At this point you have a Dockerized Flask application running. Congrats!

By the way, if you tried to submit the contact form and you received a CSRF token
error then 
[check out how to fix this problem]({% post_url 2016-06-11-fix-missing-csrf-token-issues-with-flask %}){:target="_blank"}.
Spoiler alert: it's a bug with Chrome.

### Shutting things down

You'll want to goto your Docker Compose terminal tab and press `CTRL+C`. Then for
good measure, type `docker-compose stop`. Sometimes Compose bugs out and won't
stop all of your containers automatically.

You could also optionally run `docker-compose rm -f` to clean up your stopped
containers. I tend to do this all the time.

#### General house keeping

If you keep building images, Docker is going to accumulate a lot of cruft. You
may notice that you even run out of disk space but you can easily prevent that.

You can remove dangling Docker images by running:  
`docker rmi -f $(docker images -qf dangling=true)`

You can also remove dangling Docker volumes by running:  
`docker volume rm $(docker volume ls -qf dangling=true)`

I recommend you run these commands at least once a week, or more if you're
really actively using Docker. I personally run them on a daily cronjob.

### Do you want to learn more about Flask?

*Build up a 4,000+ line software as a service application with Flask in stages
where I'll be at your side explaining my thought process every step of the way.*

<a class="btn green" href="{{ site.baseurl }}courses/build-a-saas-app-with-flask">
  Become a Flask Master
</a>
