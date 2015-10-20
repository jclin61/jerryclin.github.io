---
layout: post
title:  "Jekyll Serve command not working due to missing Kramdown dependency"
date:   2015-10-20 17:03:41
categories: jekyll update
---

Weeks after first post, I thought of something that I'd like to share.
As soon as I dived into my jekyll repo, I ran into an issue. 
`'jekyll serve'` doesn't work! Apparently, I am missing a Markdown dependency, Kramdown.

{% highlight ruby %}

You are missing a library required for Markdown. Please run:
  $ [sudo] gem install kramdown
  Conversion error: Jekyll::Converters::Markdown encountered an error while converting '_posts/2015-09-10-welcome-to-jekyll.markdown/#excerpt':
                    Missing dependency: kramdown
             ERROR: YOUR SITE COULD NOT BE BUILT:
                    ------------------------------------
                    Missing dependency: kramdown

{% endhighlight %}

That's strange, I thought. My first post experience was smooth, and I certinaly don't recall running into this problem. At the same time, all I did was install jekyll, add a few sentences to first post, and push the repo. I may have not even tested locally. 

Anyway, I followed `sudo gem install kramdown` and specifically included this gem in my gemfile right below `gem 'github-pages`.

{%highlight ruby%}

source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']
gem 'kramdown', versions['kramdown']

{%endhighlight%}

Then I ran `bundle install` to make sure Kramdown is installed.

This should have worked, but running `jekyll serve` still tells me I am missing 'kramdown' depenency.
What in the world?!

Turns out, the best practice is to execute `jekyll serve` via an executable from bundler as such:
`bundle exec jekyll install` as addressed from <a href="http://bundler.io/">bundler.io</a>.

Local server started without hiccups, and I lost my original thought that I wanted to share before running into this issue. 

Oh well. At least jekyll's working!
