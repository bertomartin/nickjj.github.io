---
layout: post
title: 'Dockerize a Rails 5, Postgres, Redis, Sidekiq and Action Cable Application'
tags: [ruby-on-rails, docker, tutorial]
excerpt:
  Learn how to install and use Docker to run a Rails 5, Postgres, Redis,
  Sidekiq and Action Cable app in development with Docker Compose.
---

After this tutorial, you'll understand what the benefits of using Docker are
and will be able to:

- Install Docker on all major platforms in 5 minutes or less
- Run an example Rails 5+ app that uses a bunch of best practices
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

## Creating the Rails application

The focus of this blog post is on Dockerizing a Rails application that has a
number of moving parts. We could use `rails new` to create a new project and
build it up, but it would be faster just to use a pre-made application instead.

We're going to be using a base application provided by orats, which is an
[open source tool to generate opinionated Rails projects](https://github.com/nickjj/orats){:target="_blank"}.

If you want to learn more about what this base application has to offer, then
I recommend reading the
[orats README file](https://github.com/nickjj/orats){:target="_blank"} for that.
This post will cover just the Docker specific side of things.

### Install orats

Since you're very likely a Ruby developer, you have Ruby installed on your
work station so installation is as simple as `gem install orats`.

### Generate a new project

```sh
# Feel free to generate the project anywhere you want.
orats new /tmp/my_dockerized_app
```

### Open the project in your favorite code editor

```sh
# Move into the project's directory
cd /tmp/my_dockerized_app

# Open the project with your favorite editor (mine is Sublime)
subl .
```

Feel free to use whatever editor you want, but if you like Sublime Text 3 and
you want to configure it for Rails, Docker and more then check out my post on
[25 Sublime Text 3 Packages for Polyglot Programmers]({% post_url 2016-04-13-25-sublime-text-3-packages-for-polyglot-programmers %}){:target="_blank"}.

## Dockerize the Rails application

There's a few things we need to do to Dockerize the application.

### Logging

In order for logs to function properly, Docker expects your application or
process to log to STDOUT. This is a very good idea because the concept of
managing log files will now be de-coupled from your Rails application.

You can choose to have Docker write those log entries to syslog or another local
service running on your server, or you can ferry the log output over to a third
party service such as Loggly.

In either case, you need to make a small adjustment to your Rails app.

```ruby
# app/config/application.rb : Lines 21-24

logger           = ActiveSupport::Logger.new(STDOUT)
logger.formatter = config.log_formatter
config.log_tags  = [:subdomain, :uuid]
config.logger    = ActiveSupport::TaggedLogging.new(logger)
```

In the orats base project, I've decided to set up logging in the `application.rb`
file because it will be common to all environments.

We're just setting Rails up to log to STDOUT and then we also set up a custom
formatter to include both the subdomain and uuid in each log entry.

I like doing this because it makes filtering logs very simple -- especially
when your application grows in size and has many moving parts.


### Docker specific files

The root of the project has a few files that are related to Docker:

```sh
nick@oriath:/tmp/my_dockerized_app ⚡ ls -la
-rw-rw-r--  1 nick nick    3507 Jul  7 10:50 .env
-rw-rw-r--  1 nick nick    1032 Jul  7 10:50 docker-compose.yml
-rw-rw-r--  1 nick nick    4353 Jul  7 10:50 Dockerfile
-rw-rw-r--  1 nick nick     49  Jul  7 10:50 .dockerignore
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
a Docker image that has a Debian Jessie base, all of the Rails code and by
default it will run the Puma app server.

Let's break down what each line is doing:

```sh
FROM ruby:2.3-slim
# Docker images can start off with nothing, but it's extremely
# common to pull in from a base image. In our case we're pulling
# in from the slim version of the official Ruby 2.3 image.
#
# Details about this image can be found here:
# https://hub.docker.com/_/ruby/
#
# Slim is pulling in from the official Debian Jessie image.
#
# You can tell it's using Debian Jessie by clicking the
# Dockerfile link next to the 2.3-slim bullet on the Docker hub.
#
# The Docker hub is the standard place for you to find official
# Docker images. Think of it like GitHub but for Docker images.

MAINTAINER Nick Janetakis <nick.janetakis@gmail.com>
# It is good practice to set a maintainer for all of your Docker
# images. It's not necessary but it's a good habit.

RUN apt-get update && apt-get install -qq -y --no-install-recommends \
      build-essential nodejs libpq-dev
# Ensure that our apt package list is updated and install a few
# packages to ensure that we can compile assets (nodejs) and
# communicate with PostgreSQL (libpq-dev).

ENV INSTALL_PATH /my_dockerized_app
# The name of the application is my_dockerized_app and while there
# is no standard on where your project should live inside of the Docker
# image, I like to put it in the root of the image and name it
# after the project.
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
# having to CD into the /my_dockerized_app folder every time would be
# lame, so instead we can set the WORKDIR to be /my_dockerized_app.
#
# By doing this, Docker will be smart enough to execute all
# future commands from within this directory.

COPY Gemfile Gemfile.lock ./
# This is going to copy in the Gemfile and Gemfile.lock from our
# work station at a path relative to the Dockerfile to the
# my_dockerized_app/ path inside of the Docker image.
#
# It copies it to /my_dockerized_app because of the WORKDIR being set.
#
# We copy in our Gemfile before the main app because Docker is
# smart enough to cache "layers" when you build a Docker image.
#
# You see, each command we have in the Dockerfile is going to be
# ran and then saved as a separate layer. Docker is smart enough
# to only re-build pieces that change, in order from top to bottom.
#
# This is an advanced concept but it means that we'll be able to
# cache all of our gems so that if we make an application code
# change, it won't re-run bundle install unless a gem changed.

RUN bundle install --binstubs
# We want binstubs to be available so we can directly call sidekiq and
# potentially other binaries as command overrides without depending on
# bundle exec.
# This is mainly due for production compatibility assurance.

COPY . .
# This might look a bit alien but it's copying in everything from
# the current directory relative to the Dockerfile, over to the
# /my_dockerized_app folder inside of the Docker image.
#
# We can get away with using the . for the second argument because
# this is how the unix command cp (copy) works. It stands for the
# current directory.

RUN bundle exec rake RAILS_ENV=production DATABASE_URL=postgresql://user:pass@127.0.0.1/dbname ACTION_CABLE_ALLOWED_REQUEST_ORIGINS=foo,bar SECRET_TOKEN=dummytoken assets:precompile
# Provide a dummy DATABASE_URL and more to Rails so it can pre-compile
# assets. The values do not need to be real, just valid syntax.
#
# If you're saving your assets to a CDN and are working with multiple
# app instances, you may want to remove this step and deal with asset
# compilation at a different stage of your deployment.

VOLUME ["$INSTALL_PATH/public"]
# In production you will very likely reverse proxy Rails with nginx.
# This sets up a volume so that nginx can read in the assets from
# the Rails Docker image without having to copy them to the Docker host.

CMD puma -C config/puma.rb
# This is the command that's going to be ran by default if you run the
# Docker image without any arguments.
#
# In our case, it will start the Puma app server while passing in
# its config file.
```

At this point we could build the image and you'd be able to access the Rails app,
but let's avoid doing that for now.

#### .dockerignore

Let's first look at the next file which is the `.dockerignore` file.

```sh
.git
.dockerignore
.byebug_history
/log/*
/tmp/*
```

When we copied in all of the files from our current directory into the Docker
image with the `COPY . .` command, it's going to copy literally everything.

That's not the best idea in the world because if your project is a git repo
you're going to have a TON of extra data. You should strive to have the smallest
Docker images you can within reason.

The `.dockerignore` file is very similar to a `.gitignore` file. It lets you
black list certain folders or files from being included.

#### docker-compose.yml

Docker Compose is an official tool supplied by Docker. At its core, it's a
utility that lets you "compose" Docker commands.

Before you can appreciate just how useful this tool is, we need to go over what
life would be like without Docker Compose.

Let's say say you wanted to get your workstation to the point where you could
run the Rails application. You would have to type all of these commands:

*You don't need to follow along but read the comments!*

```sh
# [Docker-enabled terminal tab 1]
#
# Create a default network to allow Docker containers
# to talk to each other.
docker network create my_dockerized_app

# Pull down Redis from the Docker hub.
docker pull redis:3.2-alpine

# Build the my_dockerized_app image for the website.
docker build -t my_dockerized_app_website .

# Run the Redis image that:
# 1. Has a Docker container name of my_dockerized_app_redis.
# 2. Has a named volume to persist its data.
# 3. Is a part of the my_dockerized_app network.
# 4. Maps port 6379 on your work station to port 6379 inside the
#    Docker container.
# 5. Overrides the Redis CMD to run Redis with a password.
docker run --name my_dockerized_app_redis -v redis:/var/lib/redis/data \
   --net my_dockerized_app -p 6379:6379 \
   redis:3.2-alpine redis-server --requirepass yourpassword

# [Docker-enabled terminal tab 2]
#
# Run the Postgres image that:
# 1. Has a Docker container name of my_dockerized_app_postgres.
# 2. Has a named volume to persist its data.
# 3. Is a part of the my_dockerized_app network.
# 4. Maps port 5432 on your work station to port 5432 inside the
#    Docker container.
# 5. Sets both the `POSTGRES_USER` and `POSTGRES_PASSWORD` env values.
docker run --name my_dockerized_app_postgres \
   -v postgres:/var/lib/postgresql/data \
   --net my_dockerized_app -p 5432:5432 \
   -e POSTGRES_USER=my_dockerized_app \
   -e POSTGRES_PASSWORD=yourpassword \
   postgres:9.5

# [Docker-enabled terminal tab 3]
#
# Run the Rails application that:
# 1. Has a Docker container name of my_dockerized_app_website.
# 2. Volume mounts in the current working directory to
#    /my_dockerized_app inside of the container, which will override
#    what was built in the Docker image.
#    This is a key concept that will let you actively develop your
#    application without having to re-build your Docker image
#    on each change.
# 3. Maps port 3000 on your work station to port 3000 inside the
#    Docker container.
# 4. Reads in environment variables from the `.env` file.
# 5. Is a part of the my_dockerized_app network.
docker run --name my_dockerized_app_website \
  -v $PWD:/my_dockerized_app -p 3000:3000 \
  --env-file .env \
  --net my_dockerized_app my_dockerized_app_website

# [Docker-enabled terminal tab 4]
#
# Run the Sidekiq background worker that:
# 1. Has a Docker container name of my_dockerized_app_sidekiq.
# 2. Volume mounts in the current working directory to
#    /my_dockerized_app inside of the container, which will override
#    what was built in the Docker image.
#    This is a key concept that will let you actively develop your
#    application without having to re-build your Docker image
#    on each change.
# 3. Reads in environment variables from the `.env` file.
# 4. Is a part of the my_dockerized_app network.
# 5. Overrides the Puma app CMD to run Sidekiq instead.
docker run --name my_dockerized_app_sidekiq \
  -v $PWD:/my_dockerized_app --env-file .env \
  --net my_dockerized_app my_dockerized_app_website \
  sidekiq -C config/sidekiq.yml.erb

# [Docker-enabled terminal tab 5]
#
# Run the Action Cable server that:
# 1. Has a Docker container name of my_dockerized_app_cable.
# 2. Volume mounts in the current working directory to
#    /my_dockerized_app inside of the container, which will override
#    what was built in the Docker image.
#    This is a key concept that will let you actively develop your
#    application without having to re-build your Docker image
#    on each change.
# 3. Maps port 28080 on your work station to port 28080 inside the
#    Docker container.
# 4. Reads in environment variables from the `.env` file.
# 5. Is a part of the my_dockerized_app network.
# 6. Overrides the Puma app CMD to run Action Cable instead.
docker run --name my_dockerized_app_cable \
  -v $PWD:/my_dockerized_app -p 28080:28080 --env-file .env \
  --net my_dockerized_app my_dockerized_app_website \
  puma -p 28080 cable/config.ru
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
  postgres:
    image: 'postgres:9.5'
    environment:
      POSTGRES_USER: 'my_dockerized_app'
      POSTGRES_PASSWORD: 'yourpassword'
    ports:
      - '5432:5432'
    volumes:
      - 'postgres:/var/lib/postgresql/data'

  redis:
    image: 'redis:3.2-alpine'
    command: redis-server --requirepass yourpassword
    ports:
      - '6379:6379'
    volumes:
      - 'redis:/var/lib/redis/data'

  website:
    depends_on:
      - 'postgres'
      - 'redis'
    build: .
    ports:
      - '3000:3000'
    volumes:
      - '.:/my_dockerized_app'
    env_file:
      - '.env'

  sidekiq:
    depends_on:
      - 'postgres'
      - 'redis'
    build: .
    command: sidekiq -C config/sidekiq.yml.erb
    volumes:
      - '.:/my_dockerized_app'
    env_file:
      - '.env'

  cable:
    depends_on:
      - 'redis'
    build: .
    command: puma -p 28080 cable/config.ru
    ports:
      - '28080:28080'
    volumes:
      - '.:/my_dockerized_app'
    env_file:
      - '.env'

volumes:
  redis:
  postgres:
```

We're using `version: 2` because as of Docker Compose 1.6+, Docker Compose
introduced a new syntax that is going to be used moving forward.

Then we have a `services` namespace that lets us define our services. They are
the same services we ran manually.

As you can see, the properties we define match up with the command line flags
that we passed in to various Docker commands earlier.

The only new thing is `depends_on` which is a Docker Compose feature that will
start the depended on services before starting the service that depends on it.

In other words, `postgres` and `redis` containers will be started before the
`website`, `sidekiq` and `cable` containers get started.

Lastly, we have a `volumes` namespace for our named volume(s).

#### .env

This file isn't technically part of Docker, but it's partly used by Docker
Compose and the Rails application.

By default Docker Compose will look for an `.env` file in the same directory
as your `docker-compose.yml` file.

We can set various environment variables here, and you can even add your custom
environment variables here too if your application uses ENV variables.

```sh
COMPOSE_PROJECT_NAME=my_dockerized_app
```

By setting the `COMPOSE_PROJECT_NAME` to `my_dockerized_app`, Docker Compose
will automatically prefix our Docker images, containers, volumes and networks
with `mydockerizedapp`.

It just so happens that Docker Compose will strip underscores from the name.

There's plenty of other values in this `.env` file but most of them are custom
to the Rails application. We'll go over a few Docker related values in a bit.

## Run the Ruby on Rails application

You can run everything by typing: `docker-compose up --build`. Docker Compose
has many different sub-commands and flags. You'll definitely want to check them
out on your own.

After the `up` command finishes, open up a new terminal tab and check out what
was created on your behalf.

#### Docker images

Run `docker images`:

```sh
mydockerizedapp_cable     latest              ...         579 MB
mydockerizedapp_sidekiq   latest              ...         579 MB
mydockerizedapp_website   latest              ...         579 MB
postgres                  9.5                 ...         265.8 MB
redis                     3.2-alpine          ...         29.02 MB
ruby                      2.3-slim            ...         285.1 MB
```

Docker Compose automatically pulled down Redis and Python for you, and then
built the website, sidekiq and cable images for you.

#### Docker containers

Run `docker-compose ps`:

```sh
Name                        State   Ports          
-------------------------------------------------------------------
mydockerizedapp_cable_1      ...   Up      0.0.0.0:28080->28080/tcp 
mydockerizedapp_postgres_1   ...   Up      0.0.0.0:5432->5432/tcp   
mydockerizedapp_redis_1      ...   Up      0.0.0.0:6379->6379/tcp   
mydockerizedapp_sidekiq_1    ...   Up                               
mydockerizedapp_website_1    ...   Up      0.0.0.0:3000->3000/tcp 
```

Docker Compose automatically named the containers for you, and it appended a
`_1` because it's running 1 instance of the Docker image.

Docker Compose supports scaling but that goes beyond the scope of this tutorial.

We can also see which ports the services are using.

#### Docker volumes

Run `docker volume ls`:

```sh
DRIVER              VOLUME NAME
local               mydockerizedapp_postgres
local               mydockerizedapp_redis
```

Docker Compose automatically created the named volume for Postgres and Redis.

Run `docker volume --help` to see what else you can do on your own.

#### Docker networks

Run `docker network ls`:

```sh
NETWORK ID          NAME                      DRIVER
...                 bridge                    bridge
...                 host                      host
...                 none                      null
...                 mydockerizedapp_default   bridge
```

Docker Compose created the network for you when you ran `up`. I recommend you
run `docker network --help` to see what else you can do on your own.

If you were to look at the `.env` file and check out this line:

```sh
REDIS_CACHE_URL=redis://:yourpassword@redis:6379/0/cache
```

You'll notice that we're referencing `redis` as the actual Redis host name.

We can do this because of the Docker network that was created for us. Our Redis
service is defined as `redis` in the `docker-compose.yml` file, so we're able
to reference it by name as a legit host name.

This works because Docker is managing a DNS server for you on your behalf.

### Viewing the site

If you installed Docker through the Docker Toolbox then you'll need to make 3
quick changes to the `.env` file. If you're running Docker natively then you
can access `http://localhost:3000` right now.

#### Docker Toolbox users need to make 3 changes to the `.env` file

```sh
# Open the .env file and find these values:
ACTION_MAILER_HOST=localhost:3000
ACTION_CABLE_FRONTEND_URL=ws://localhost:28080
ACTION_CABLE_ALLOWED_REQUEST_ORIGINS=http:\/\/localhost*

# Replace `localhost` with your Docker Machine IP address:
ACTION_MAILER_HOST=192.168.99.100:3000
ACTION_CABLE_FRONTEND_URL=ws://192.168.99.100:28080
ACTION_CABLE_ALLOWED_REQUEST_ORIGINS=http:\/\/192.168.99.100*
```

Toolbox users need to change a few instances of `localhost` to `192.168.99.100`
or whatever your Docker Machine IP address is. You can determine your IP by
running `docker-machine ip` from a Docker-enabled terminal.

This is because you don't have Docker running natively on your system. It also
means you'll need to access `http://192.168.99.100:3000` in your browser.

At this point you'll notice that it throws an error saying the database does
not exist. No worries, that's expected right? We haven't reset our database yet.

### Interacting with the Rails application

This section of the blog post will serve 2 purposes. It will show you how to
run Rails commands through Docker, and also shows you how to initialize a Rails
database.

*Run both of the commands below in a new Docker-enabled terminal tab*

#### Reset the database

<small>
  <code>
    docker-compose exec --user "$(id -u):$(id -g)" website rails db:reset
  </code>
</small>

- If you're on OSX or Windows, do not include the `--user flag`

#### Migrate the database

<small>
  <code>
    docker-compose exec --user "$(id -u):$(id -g)" website rails db:migrate
  </code>
</small>

- If you're on OSX or Windows, do not include the `--user flag`

#### What's going on with the above commands?

Docker Compose has an `exec` command which lets you execute commands on an
already running container. We're running commands on the `website` container.

The `--user "$(id -u):$(id -g)"` flag ensures that any files being generated
by the `exec` command end up being owned by your user rather than root.

You only need to add this flag if you're running Docker natively.

#### Common theme between the above commands?

After defining which container will run the command, all we have to do is pass
in the actual command we want to run.

In this case, we're running standard `rails` commands. With Rails 5+, you can
perform `rake` tasks through the `rails` binary.

Every Rails command that you would normally run without Docker can be ran in
the above way. For example if you wanted to generate a new controller:

##### Add a new controller

<small>
  <code>
    docker-compose exec --user "$(id -u):$(id -g)" website rails g controller Hi
  </code>
</small>

##### Remove that controller

<small>
  <code>
    docker-compose exec --user "$(id -u):$(id -g)" website rails d controller Hi
  </code>
</small>

#### A live development environment

Since we have volumes set up in `docker-compose.yml` you'll be able to
actively develop your application as if it were running natively on your OS.

Try going to `app/views/pages/home.html.erb`, then make a change to the file.
All you have to do is save the file and reload your browser to see the changes.

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

### Conclusion

Docker is awesome. Now you can run your projects on other platforms without
having to worry about dependencies and platform specific gotchas.

You can even deploy them to production with minimal fuss.

### Deploy a load balanced and secure Dockerized Rails app on AWS

*Learn what it takes to deploy a scalable web application on Amazon Web Services
(AWS) with Docker. No prior AWS knowledge needed!*

<a class="btn green" href="{{ site.baseurl }}courses/scaling-docker-on-aws">
  Deploy your app on AWS
</a>
