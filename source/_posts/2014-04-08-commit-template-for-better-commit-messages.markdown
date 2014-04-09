---
layout: post
title: "Commit template for better commit messages"
date: 2014-04-08 17:34:29 +0100
comments: true
categories: 
- Git
---

Writing good commit messages should be an everyday commitment, but it can be sometimes difficult to stay self-disciplined, expecially on your personal project or during rush hours. This behaviour is well represented by xkcd:

![Git commit by xkcd: http://xkcd.com/1296/](http://imgs.xkcd.com/comics/git_commit.png "Git Commit by xkcd")

*Source: [http://xkcd.com/1296/](http://xkcd.com/1296/)*

A good solution is to create a default commit message, which will be used every time a commit is supposed to be done. Thanks to this message template you get used to the format and keep a good habit, and the configuration is pretty easy to do.

<!-- more -->

The configuration steps are well described on the [git-scm website, chapter 7.1 Customizing Git - Git Configuration, section *commit.template*](http://git-scm.com/book/en/Customizing-Git-Git-Configuration)

## Create a template

Create a file at `$HOME/.gitmessage.txt` if you want it global, or in your project's folder if you want it specific to your project.  
In this file, specify the template you would like to see everytime you commit.

Example (Not saying it's the best one):

```
[theme] subjectline (keep it short)

WhatHappened
```

Some discussion about the message template and what a commit message should be can be found on the [Erlang/Otp wiki](https://github.com/erlang/otp/wiki/Writing-good-commit-messages) or on the [tbaggery blog](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)

## Configure Git

Then configure Git to use you brand new template, using the commit.template parameter.

If it's for all your project, run:
{% codeblock lang:bash %}
git config --global commit.template $HOME/.gitmessage.txt
{% endcodeblock %}

If it specific to your Git based project directoy, assuming you have saved the template in this directory:

{% codeblock lang:bash %}
cd project_directory/
git config --local commit.template .gitmessage.txt
{% endcodeblock %}

## Commit

And then commit as usual but **without** using the `-m` flag, so your default `$EDITOR` will show up with the text from the template prepopulated.

If you keep replacing the values and filling the blanks of the template, you will quickly get use to the format. It's then a matter of time before you disable the template and keep going with your new good habit.
