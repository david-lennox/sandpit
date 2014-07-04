---
layout: post
title:  "Creating a Jekyll Blog"
date:   2014-07-04
comments: true
---

## Process in a Nutshell

Start at the [GitHub help page](https://help.github.com/articles/using-jekyll-with-pages).

In addition to supporting regular HTML content, GitHub Pages support Jekyll, a simple, blog aware static site generator written by our own Tom Preston-Werner.

So Jekyll is a simple templating engine (I think).

Jekyll is a Ruby application that you point at a folder and it will:

* Convert all the files in the folder to a static web site based on simple conventions and the Liquid templating language.
* Serve the generated site at localhost:4000

You do not need to install Jekyll on your local machine because GitHub will run the conversions and serve the site. It is however strongly recommended to have it on your local machine for debugging.

### To Setup Locally

Installed RVM on Linux machine (Ruby Version Manager)

To install Ruby on Ubuntu, I followed the instructions in [this StackOverflow post](http://stackoverflow.com/questions/9056008/installed-ruby-1-9-3-with-rvm-but-command-line-doesnt-show-ruby-v).

This installed Ruby 2.1.2.

Then `gem install bundler`

Follow GitHub instructions to create a gh-pages branch for any of your repositories. This is where the Jekyll site will be pushed to and served from.

Every GitHub account can also have one Jekyll site not associated with a repo.

Clone the Git Repo to a local folder, checkout the gh-pages branch.

Create Gemfile in top level folder (sibling to .git) with content:

    source 'https://rubygems.org'
    gem 'github-pages'

Then at the command line:

    bundle install

This installs Jekyll and some dependencies. GitHub strongly recommends using bundler and running Jekyll with:

    path/to/site$ bundle exec jekyll serve

This is obviously dependent on the previous commands.

### Add Disqus Commenting Service

Can be done in about 5 minutes.

* Sign up to Disqus and register a new site. They will provide a shortname.
* Add the shortname to the site properties in the _config.yml file.
* If you start with a Jekyll template of some kind the Disqus code will probably be there already, otherwise cut and paste it. For Jekyll we use the 'Universal Code'.

