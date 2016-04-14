---
layout: post
title: '25 Sublime Text 3 Packages for Polyglot Programmers'
tags: [dev-environment]
excerpt:
  A recap and showcase of 25 Sublime Text 3 packages I use on a day to day
  basis as a developer who uses multiple technologies.
---

It's 2016, so chances are you know more than 1 programming language and most
web based projects tend to require looking at a number of different file types.

If you're wondering why I use Sublime, then check out my post on
[Why Sublime Text 3 Is Still My Preferred Code Editor]({% post_url 2016-04-13-why-sublime-text-3-is-still-my-preferred-code-editor %}).

## What do I use Sublime for?

I find myself bouncing around projects while doing consulting work and these
are the main file types I deal with:

#### Programming languages and web frameworks
- Python / Flask
- Ruby / Ruby on Rails

#### Templating languages
- Jinja2
- ERB
- Liquid

#### General web development
- HTML
- CSS
- SCSS
- JavaScript
- JSON

#### General system admin and operations tasks
- Git
- Bash
- YAML
- Markdown
- Docker
- nginx configs

## Package list

Each package is linked to its official GitHub repo and the link name is the
package name itself if you want to install it directly with
<a target="_blank" href="https://packagecontrol.io/">Package Control</a>.

*There's a bunch of screenshots at the bottom of the post.*

### Theme

#### <a target="_blank" href="https://github.com/Miw0/SoDaReloaded-Theme">Theme - SoDaReloaded</a>

SodaReloaded comes with both a light and dark version. It differs from the Soda
theme by offering sidebar icons and a few other tweaks.

### Color scheme

#### <a target="_blank" href="https://github.com/buymeasoda/soda-theme/#bonus-options">Espresso Soda</a>

This is a light color scheme, but the link above also includes a dark variant.
Both schemes were created by the original Soda theme's author.

### General packages

#### <a target="_blank" href="https://github.com/wbond/sublime_terminal">Terminal</a>

Rather than try to mimic a terminal inside of Sublime this handy package lets
you launch your system's terminal through Sublime.

You have the option of using a hotkey to launch a terminal at the path of the
current file you're editing, or you can right click anywhere in your sidebar.

#### <a target="_blank" href="https://github.com/condemil/Gist">Gist</a>

In about 60 seconds you'll be set up to be able to post both public or private
gists. You can gist a full file, or selected text.

It even supports updating gists and multiple files.

#### <a target="_blank" href="https://github.com/jisaacks/GitGutter">GitGutter</a>

Ever wondered which lines in a file are different vs what's been commit to git?

If so, this is the package for you because it will render icons in your gutter
to show you different types of changes.

#### <a target="_blank" href="https://github.com/titoBouzout/SideBarEnhancements">SideBarEnhancements</a>

The default sidebar right click menu in Sublime is decent but this package
takes it to the next level by supplying a number of handy features.

#### <a target="_blank" href="https://github.com/vaanwd/Zeal">Zeal</a>

*Requires installing Zeal (check the link below)*

<a target="_blank" href="https://zealdocs.org/">Zeal</a> is a free offline
documentation viewer. You can find documentation for about 200 technologies and
it stays up to date. You can pick what you want installed.

This package integrates things with Sublime so all you have to do is mouse over
a function or word in your editor and hit a hotkey to launch its documentation.

If you're on OSX you can use
<a target="_blank" href="https://kapeli.com/dash">Dash</a> instead.

#### <a target="_blank" href="https://github.com/SublimeText-Markdown/MarkdownEditing">MarkdownEditing</a>

Without question, this is the best Markdown experience I've seen in any editor.

It's one of the more interesting Sublime packages I've seen because it alters
the code editing experience in a fun but familiar way.

### Web development packages

#### <a target="_blank" href="https://github.com/ggordan/GutterColor">Gutter Color</a>

*Requires installing Imagemagick (check the README linked above)*

It's useful to be able to see what colors your CSS and SCSS are at a glance.
This package draws a color preview in the gutter when it find a line that
contains a color.

#### <a target="_blank" href="https://github.com/mrmartineau/HTML5">HTML5</a>

This package adds syntax coloring and snippet support for HTML5 elements.

#### <a target="_blank" href="https://github.com/JasonMortonNZ/bs3-sublime-plugin">Bootstrap 3 snippets</a>

I don't know about you, but I always end up referencing Bootstrap's documentation
for certain components.

That lifestyle is a thing of the past because this package adds a bunch of
snippets to easily access every Bootstrap 3 component.

#### <a target="_blank" href="https://github.com/MarioRicalde/SCSS.tmbundle/tree/SublimeText2">SCSS</a>

This package adds syntax coloring and snippet support for SCSS.

#### <a target="_blank" href="https://github.com/kudago/jinja2-tmbundle">Jinja2</a>

This package adds syntax coloring and snippet support for Jinja2.

#### <a target="_blank" href="https://github.com/matthewrobertson/ERB-Sublime-Snippets">ERB Snippets</a>

This package adds syntax coloring and snippet support for ERB.

### System admin and operations packages

#### <a target="_blank" href="https://github.com/asbjornenge/Docker.tmbundle">Dockerfile Syntax Highlighting</a>

This package adds syntax highlighting support for Docker files.

#### <a target="_blank" href=" https://github.com/brandonwamboldt/sublime-nginx">nginx</a>

This package adds syntax highlighting support for nginx config files.

### Linters

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter3">SublimeLinter</a>

This package is more like a base framework for other packages to use. This is
the defacto standard linting base package to use with Sublime.

You would combine this package with specific linters (listed below).

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-shellcheck">SublimeLinter-shellcheck</a>

*Requires installing shellcheck (check the README linked above)*

This linter will check your bash scripts for syntax errors and visually warn
you if it finds anything questionable.

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-html-tidy">SublimeLinter-html-tidy</a>

*Requires installing tidy (check the README linked above)*

This linter will check your HTML for syntax errors and visually warn you if it
finds anything questionable.

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-csslint">SublimeLinter-csslint</a>

*Requires installing csslint (check the README linked above)*

This linter will check your CSS for syntax errors and visually warn you if it
finds anything questionable.

#### <a target="_blank" href="https://github.com/attenzione/SublimeLinter-scss-lint">SublimeLinter-contrib-scss-lint</a>

*Requires installing scss_lint (check the README linked above)*

This linter will check your SCSS for syntax errors and visually warn you if it
finds anything questionable.

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-jshint">SublimeLinter-jshint</a>

*Requires installing jshint (check the README linked above)*

This linter will check your JavaScript for syntax errors and visually warn you
if it finds anything questionable.

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-json">SublimeLinter-json</a>

*Requires installing jshint (check the README linked above)*

This linter will check your JSON for syntax errors and visually warn you if it
finds anything questionable.

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-flake8">SublimeLinter-flake8</a>

*Requires installing flake8 (check the README linked above)*

This linter will check Python files for syntax errors and visually warn you if
it finds anything questionable.

#### <a target="_blank" href="https://github.com/SublimeLinter/SublimeLinter-rubocop">SublimeLinter-rubocop</a>

*Requires installing rubocop (check the README linked above)*

This linter will check Ruby files for syntax errors and visually warn you if
it finds anything questionable.

## Sublime settings

All of my Sublime settings are included in this gist:

{% gist nickjj/8f5f95d315fe37e293c57f2d6e90cd2d %}

## Screenshots

Text is nice to read, but being able to see how these packages work without
having to install them yourself is even better.

Here's a few screenshots that show off some of the packages:

### Jinja

In addition to syntax highlighting it also includes a bunch of snippets.

![Sublime Text 3 - Jinja]({{ site.baseurl}}assets/img/blog/st3-jinja.jpg "Jinja")

### JavaScript linting

Pay close attention to the status bar text. That is happening in real-time.

![Sublime Text 3 - JavaScript linting]({{ site.baseurl}}assets/img/blog/st3-js-lint.jpg "JavaScript linting")

### Markdown

The text is auto-centered for less distractions while writing.

![Sublime Text 3 - Markdown]({{ site.baseurl}}assets/img/blog/st3-markdown.jpg "Markdown")

### Zeal

Highlight a keyword and hit a hotkey. It pops up for any language / keyword!

![Sublime Text 3 - Zeal]({{ site.baseurl}}assets/img/blog/st3-nginx-zeal.jpg "Zeal")

### Python

Notice the lack of a colon at the end is causing the linter to yell at us.

![Sublime Text 3 - Python syntax error]({{ site.baseurl}}assets/img/blog/st3-python-syntax-error.jpg "Python syntax error")

### Git Gutter

Changes to the file which differ from the git history will show up in the sidebar.

![Sublime Text 3 - Ruby git gutter]({{ site.baseurl}}assets/img/blog/st3-ruby-git-gutter.jpg "Ruby git gutter")

### Terminal

Launch a terminal at the current file or anywhere in the sidebar (hotkeys work too).

![Sublime Text 3 - Terminal]({{ site.baseurl}}assets/img/blog/st3-shell-terminal.jpg "terminal")

### Dark Theme / Color Scheme

Here's what Soda Reloaded and its dark color scheme look like.

![Sublime Text 3 - Dark]({{ site.baseurl}}assets/img/blog/st3-dark.jpg "dark")
