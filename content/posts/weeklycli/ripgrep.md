---
title: Weekly CLI Tool - ripgrep
date: 2021-06-11
draft: false
authors:
  - couchllama

tags:
  - CLI Tools

geekblogToC: 3

geekblogAnchor: true
---

There’s a number of grep alternatives, including [The Silver Searcher
(ag)](https://github.com/ggreer/the_silver_searcher) and
[ack](https://github.com/beyondgrep/ack3). The one I use most frequently is
[ripgrep](https://github.com/BurntSushi/ripgrep). Ripgrep is one of the fastest
text search tools and is a great alternative to grep when you’re dealing with
git repos. It’s available from most modern distro’s package managers. By
default ripgrep will determine if you’re in a git repo and ignore files in
.gitignore. It also ignores binary files and does a recursive search into all
subdirectories.

Here’s some examples for using ripgrep:

Ignore case while searching for a string:

    rg -i [STRING]

Ignore case if the string you’re searching for is all lowercase:

    rg -S [STRING]

Search files in the directory, including files in .gitignore:

    rg -u [STRING]

Only search for a string in files ending in .md:

    rg -g '\*.md' [STRING]

Another way to search for markdown files is to use types. `rg --type-list` will
show you all the types available and what globs they search for. For example,
for markdown it’ll search files matching these globs: \*.markdown, \*.md,
\*.mdown, and \*.mkdn.

    rg -t md [STRING]

You can also do the opposite by using a capital T instead. This will search for
all files except ones considered markdown:

    rg -T md [STRING]

If the type you want isn't listed then you can crate your own by adding using a
configuration file.

To use a config file you need to set the `RIPGREP_CONFIG_PATH` variable to point
to the ripgrep config file (`export RIPGREP_CONFIG_PATH=$HOME/.config/.ripgreprc`).
Here’s an example where the type foo matches the file foobar, files ending in
.foo, and .bar:

    --type-add foo:foobar
    --type-add foo:\*.{foo,bar}

For a more through walkthrough of the things you can use ripgrep for see the
[ripgrep user guide](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md).
