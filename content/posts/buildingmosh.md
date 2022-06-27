---
title: Building Mosh from Master
date: 2021-06-11
description: How to build mosh from source.
draft: false
authors:
  - couchllama

tags:
  - CLI Tools
  - iPad

geekblogToC: 3

geekblogAnchor: true
---

The first thing you want to do when setting up a server to use with blink shell
is to install mosh. I suggest building mosh from master instead of using the
version of mosh bundled with your OS. The latest Mosh release is from July 22, 2017. In fact, as of this post the last time the mosh master branch was updated
was on May 17, 2020. While mosh appears to be a dead project, it’s still
the best option we have for managing a remote shell on the iPad. This is
because unlike ssh, mosh connections can be resumed when disconnected.
This allows us to be able to switch out of blink shell without worrying
about our SSH session breaking.

I’ve included scripts for building and installing the master branch of mosh on
Ubuntu, openSUSE, and CentOS 7. If you need a script to install it on another
OS let me know and I can look at creating a guide/script.

The scripts are located [here](https://github.com/thecouchllama/mosh-build-scripts).

If you’re using MacOS then I recommend installing mosh using
[homebrew](https://brew.sh) by running

    brew install --HEAD mosh

For Arch Linux, you should install
[mosh-git](https://aur.archlinux.org/packages/mosh-git) from AUR.

After installing mosh you want to make sure that you allow connections from the
appropriate port. Mosh needs to be able to ssh into the server. It also uses
UDP ports 60000-61000 by default. you can also use `ssh -p [PORT #] [SERVER]` to
specify the UDP port to use. (For a different ssh port you’d use `mosh -ssh="ssh -p [SSH PORT]" [SERVER]`.

Generally mosh is much nicer to use than ssh. The only real downside that I've
come across is that you can’t easily forward your ssh-agent session to the
server. There’s an application called Guardian Agent that can get around this,
however I haven’t tried it yet. If you have any experience with using that then
please let us know in the comments how it is.
