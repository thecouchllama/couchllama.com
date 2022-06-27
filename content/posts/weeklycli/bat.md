---
title: Weekly CLI Tool - bat
date: 2021-06-16
draft: false
authors:
  - couchllama

tags:
  - CLI Tools

geekblogToC: 3

geekblogAnchor: true
---

![bat example](batexample.jpg)

bat is a replacement for cat that provides syntax highlighting and line
numbers. It also includes the ability to show git status, such as lines that
have been added or removed vs what's been committed. See [bat's github
page](https://github.com/sharkdp/bat) for more information. I suggest
installing the latest release from their github releases page if you're using
Ubuntu or another distro that doesn't do rolling releases for packages.

bat supports sublime text themes. I use the cobalt2 theme. To install this
theme you can clone wes bos' cobalt2 repo to the bat theme directory and then
rebuild bat's cache:

    git clone https://github.com/wesbos/cobalt2 $(bat --config-dir)/themes/cobalt2
    bat cache --build
    export BAT_THEME=”cobalt2”

I put export `BAT_THEME="cobalt2"` into my zshrc so that bat always defaults to
use the cobalt2 theme. I also set the following aliases:

    alias cat='bat -p --pager=never'
    alias catl='bat --pager=never'
    alias catp='bat'

This disables the pager and line number/gutter for cat. `catl` keeps the line
numbers/gutter and `catp` also keeps the pager.

There is also the [bat-extras](https://github.com/eth-p/bat-extras) package
that can be extracted to `/usr/local`. This provides applications that can be
used as alternatives to ripgrep, man, and watch. These alternatives include the
syntax highlighting that bat does.
