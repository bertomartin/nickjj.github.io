---
layout: post
title: 'Managing Your Passwords on the Command Line in Linux with pass'
tags: [linux, security, tutorial]
excerpt:
  Learn how to easily encrypt and organize all of your passwords on the command
  line using a great little program called 'pass'.
---

If you're new to using Linux, or perhaps watched my
[introduction screencast on how to run Linux and Windows together seamlessly]({% post_url 2016-02-23-create-an-awesome-linux-development-environment-in-windows-with-vmware %})
you might be wondering how to manage your passwords in a reasonable way.

### Access any of your passwords in about 3 seconds

Chances are you're working in a terminal very frequently, so wouldn't it make
sense to use a password manager that works from the command line?

I think so, so that's why I use this excellent tool called
<a target="_blank" href="https://www.passwordstore.org/">pass</a>.

#### `pass` uses GPG to secure your passwords

If I'm going to save my passwords in a way that another tool can read them, then
I want to be damn sure that my passwords are secure.

There's really no better way to do this than with
<a target="_blank" href="https://en.wikipedia.org/wiki/GNU_Privacy_Guard">GPG</a>.

The upside to this is the `pass` tool itself doesn't handle the encryption, and
instead it's off loaded to the industry standard GPG toolset.

The downside to this is you'll need a GPG keypair but I wouldn't even call this a
downside because you really should be encrypting your sensitive data with GPG.

#### Do you need to create a GPG keypair?

Yes, if you don't already have one, you'll need to create one.

Creating a GPG keypair is something you only do once and fortunately there's an
awesome guide on
<a target="_blank" href="https://alexcabal.com/creating-the-perfect-gpg-keypair/">
creating the perfect GPG keypair</a> which should take you about 10 minutes to
complete.

### What makes `pass` so good?

Well, let's say you wanted to get your password to Amazon. It would be as simple
as typing `pass Sites/Amazon -c` and now your password would be copied to your
clipboard for 45 seconds.

You could always omit the `-c` to have it print your password if you wanted to
do that instead. The `Sites/` bit is completely user defined too. You can
choose to namespace your passwords however you want and since they are just
folders on your drive, you can take advantage of auto-complete in the terminal.

#### Is it just for passwords?

One of the great things about `pass` is that it allows you to create multi-line
entries which allows for really interesting use cases.

Let's say you had an account on
<a target="_blank" href="http://aws.amazon.com/">Amazon Web Services (AWS)</a>
and you wanted to keep a few bits of information securely stored together, such
as:

- The e-mail address you used to register an account
- Your root account password
- A non-root user account and password
- Your secret API keys

With `pass`, setting up something like that is simple. Here's a quick demo:

<script type="text/javascript" src="https://asciinema.org/a/5jixmp9zbgwijnjiz4s02gryb.js" id="asciicast-5jixmp9zbgwijnjiz4s02gryb" async></script>

If you wanted to see all of your credentials, you would type:

```sh
nick@oriath:/tmp ⚡ pass Sites/Cloud/AWS
nonrootpassword
Email: foo@bar.com
Root password: rootpassword
Access Key ID: abc
Secret Access Key: xyz
```

If you wanted just your non-root password copied to the clipboard, you'd run
`pass Sites/Cloud/AWS -c` and it knows to copy the first line to the clipboard.

### Install and learn more about `pass`

<a target="_blank" href="https://www.passwordstore.org/">pass</a> is free to use
and you can install it on many different distributions of Linux.

Head over to
<a target="_blank" href="https://www.passwordstore.org/">https://www.passwordstore.org/</a>
to learn more.
