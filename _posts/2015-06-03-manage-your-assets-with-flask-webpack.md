---
layout: post
title: 'Manage Your Assets with Flask-Webpack'
tags: [flask, javascript, webpack, screencast, tutorial]
excerpt:
  Learn how to manage your CSS, javascript and images in your Flask projects.
---

**Update:** I gave a remote talk at [Chadev](http://chadev.com/) on this topic.

<iframe width="720" height="405" src="https://www.youtube.com/embed/rQoJcqx42pM?rel=0&iv_load_policy=3" frameborder="0"></iframe>

View the source code:  
[https://github.com/nickjj/demo-for-chattanooga-python-user-group](https://github.com/nickjj/demo-for-chattanooga-python-user-group)

---

Managing assets used to be hard. Here's 5 common things you are probably doing
every time you deploy your app:

1. Minify all your CSS and JS
2. Optimize all of your images by compressing them
3. Convert SASS/LESS/etc. into CSS
4. Convert Typescript/Coffeescript/etc. into JS
5. Tag all of your assets (including images) with md5 hashes

Doing the above and more by hand is brutal and not doing it at all is a disservice.

### Don't forget about development mode

It usually sucks to make all of the above steps happen during development because
you need to wire up half a dozen different tools, watchers and it's a bit slow.

Then you need to solve the problem of adjusting your server side templates to
make everything work. If you have a file named `foo.d5cbf1.css` and
change it, the md5 might change and now the file name would be `foo.8b7c0d.css`.

You're not going to update that by hand right? I hope not!

#### Dealing with friendly code

In development mode I want to organize my files nicely. I really like the
CommonJS module system. It's great to be able to just drop in
`var foo = require('./foo');` into my Javascript and have it all work because a
build tool compiles everything intelligently.

It's also nice to be able to use pre-processors like SASS or be able to write ES
6 Javascript and have it all compile to CSS and ES 5 on the fly almost instantly
along with outputting source maps so you can debug things properly.

### Webpack to the rescue

Webpack allows you to do the above and more. Imagine writing some React code and
while you have the page open you decide to interact with the page by adding data
to a widget you're developing.

Let's say you have a widget open and want to make a change to the Javascript.
Well, with Webpack you can set things up so it injects the change live into the
page without doing a full refresh.

Now you can instantly see your changes without touching the reload button and you
didn't even need to install a browser extensions or setup watchers.

### An introduction to Flask-Webpack

[Flask-Webpack](https://github.com/nickjj/flask-webpack) ties Webpack and Flask
together. It exposes a few global template tags so that you can work with assets
in your jinja templates and works with any wsgi server.

Everything is explained in the project's README file but I wanted to show you a
few minute demo of how you can use some of Webpack's features with a real Flask app:

<iframe width="720" height="405" src="https://www.youtube.com/embed/rO-GIB15Org?rel=0&iv_load_policy=3" frameborder="0"></iframe>

#### It's not just for Flask

Flask-Webpack is of course but the main workhorse to make all of this work is
Webpack along with a plugin I wrote for it called
[ManifestRevisionWebpackPlugin](https://github.com/nickjj/manifest-revision-webpack-plugin).

Webpack can be used with any web framework. The custom plugin also supports Ruby
on Rails by exporting a `manifest.json` file in a way that Rails understands. The
plugin was designed to allow for custom formatters to be added in.
