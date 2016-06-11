---
layout: post
title: 'Fix Missing CSRF Token Issues with Flask'
tags: [flask, tutorial]
excerpt:
  Learn how to fix bad request / CSRF token missing errors with Flask that stem
  from bugs with webkit based browsers.
---

There may come a time in your life where you're absolutely sure that you have
Flask-WTF configured properly in your application.

**You did everything the documentation stated.**

For starters, you've instantiated and exported `CsrfProtect` like so:

```python
# myapp/extensions.py
from flask_wtf import CsrfProtect

csrf = CsrfProtect()
```

You've also imported it into your `app.py` file:

```python
# myapp/app.py
from myapp.extensions import csrf
```

Then you've initialized it onto your Flask app:

```python
# myapp/app.py
def create_app():
    app = Flask(__name__)

    app.config.from_object('config.settings')

    csrf.init_app(app)
```

Finally, you've included the proper tag in your form template:

{% raw %}
```html
<form action="{{ url_for('myform') }}" method="post" role="form">
  {{ form.hidden_tag() }}
    
  <!-- The rest of your form goes here. -->
</form>
```
{% endraw %}

**Yet it still doesn't work and Flask throws a CSRF related error.**

You may have tried to debug the issue by dropping this into your form's route:

```python
print('------ {0}'.format(request.form))
```

...and to your surprise the `csrf_token` value is empty. WTF?

You've likely also opened your dev tools in your browser and went to the
resources tab to take a look at your cookies. Oddly enough, it's empty.

### What does your development environment look like?

Chances are 2 things are happening in your environment:

1. You're running Flask inside of a Docker Machine or are using Vagrant / etc.
2. You are using a webkit based browser (Chrome, Safari, Opera)

If your Flask server is not running on `localhost` then in order to get Flask
to work properly, you've likely modified the `SERVER_NAME` value somewhere.

For example, you might have something like this in `config/settings.py`:

```python
SERVER_NAME = '192.168.99.100:8000'
```

This is what I recommend my students to do in the
[Build a SAAS App with Flask course]({{ site.baseurl }}courses/build-a-saas-app-with-flask)
because we use Docker.

### What causes the Bad Request CSRF token missing error?

This problem happens because of 2 things.

Firstly, there's a bug in webkit based browsers.

[The spec for rejecting cookies](https://tools.ietf.org/html/rfc2109#section-4.3.2){:target="_blank"}
states that domain names must be a fully qualified domain name with a TLD (.com, etc.)
or be an exact IP address.

Chrome is too cool to adhere to specifications, so they decided to be more
strict and deny exact IP addresses. That means cookies won't be set if you have
an IP address based `SERVER_NAME`.

Ok, well that's pretty lame but astute readers might be thinking how does
`localhost` work because that doesn't include a TLD.

**That brings us to the second thing**, and we can blame Flask for that.

The Flask author is a very talented developer and 99.9% of the time his decisions
are for your benefit but in my opinion he screwed up with this one.

If you look at the 
[Flask source to return the cookie domain](https://github.com/pallets/flask/blob/0.11.1/flask/sessions.py#L198-222){:target="_blank"}
he makes assumptions about your development environment.

Take a look at this block of code:

```python
# Google chrome does not like cookies set to .localhost, so
# we just go with no domain then.
if rv == '.localhost':
    rv = None
```

The Flask author is definitely aware of the problem but he hard codes a fix.
I can't blame him because a lot of developers will be using `localhost` so it
fixes the problem for those developers without them having to think about it.

Nowadays Docker and virtualized development environments are much more common,
so IMO I'd like to see this turned into a Flask config option so users can set
which domain can get ignored.

### Easily fix the problem for the time being

The quickest way to fix this problem would be to modify your `/etc/hosts` file.

OSX and Linux users can find that in `/etc/hosts` and Windows users can find it
in `C:\Windows\System32\drivers\etc\hosts`.

You will need to open the file with elevated privileges, meaning you'll need
to open it with sudo or Administrator privileges.

Add this line to the bottom of the file:

`192.168.99.100 local.docker`

Keep in mind, if your development IP address is not what's listed above then
make the necessary adjustment to use yours instead.

Also feel free to change `local.docker` to anything you want, as long as it
includes a period so that it's a valid FQDN with a TLD.

For example `local.dev` or `local.host` would be valid but `localfoo` is not.

#### Updating your Flask config

The last thing you'll need to do is change your `SERVER_NAME` to match what we
just created in the `/etc/hosts` file.

You'll want to set: `SERVER_NAME = 'local.docker:8000'` or whatever you used.

At this point you're good to go and everything should work great.

### An exercise in debugging

This was an interesting issue to debug because as you may know, I'm an online
instructor and have thousands of students.

I recently created a course on Flask and I personally run Docker on Linux
natively. I also happen to use FireFox which does adhere to the spec correctly.

When I ran through the material, everything worked great but then issues started
to pour in from OSX users. OSX users would have used Docker Machine to set up
their Docker environment, so they were using IP based server names.

However, not all OSX users were reporting this issue because not everyone was
using Chrome. Needless to say, it wasn't an obvious solution, especially since
I actually had students connect to my server and successfully submit the form.

Where as, when I connected to their server it worked for me because I was using
FireFox. Then when I tried Chrome on their server it failed, and that lead me
to eventually tie in that the problem had something to do with Chrome.

Other students reported the same problem on Safari so it seems to affect webkit
in general.

The lesson here is that you should take nothing for granted when it comes to
debugging. Even the slightest change in environment can cause drastic
differences in output.

## Are you ready to dive deep with Flask and Docker?

*Join me where we'll build up a 4,000+ line Flask application in stages while I
explain my thought process every step of the way.*

<a class="btn green" href="{{ site.baseurl }}courses/build-a-saas-app-with-flask">
  Become a Flask Master
</a>
