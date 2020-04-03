---
layout: post
title: Setting up Jekyll with GitHub Pages on Linux
categories: Linux Jekyll
---

There are a lot of different ways to get a blog started. A typical Google search brings up Wordpress, buying a domain name, Tumblr, Blogger, etc. I've tried using a few of these, but none of them seemed like a good fit. I want a hobby outside of work and studies, but I'm not willing to pay monthly for it. 

I stumbled upon a [video](https://www.youtube.com/watch?v=iMmR5UVOz8Q) by [Luke Smith](https://www.youtube.com/channel/UC2eYFnH61tmytImy1mTYvhA) that talked about different ways to set up a personal website. He mentioned GitHub Pages, at this point I had not heard about it. I looked into it a little more, which introduced me to Jekyll. After doing some research on it, this is the route I decided to take.

## Benefits of GitHub Pages and Jekyll
The first obvious benefit is the integration of GitHub. You get the strength of git (version tracking and what not) with the benefit of being able to access your website and your source code from anywhere. This is nice because you can work on blog posts on any computer using GitHub's online editor (although not ideal), and can even post to your blog from anywhere.

The second, and not so obvious benefit, is the integration of Jekyll. Jekyll is a static website generator. It converts markdown files into html and themes it to your liking. This makes very speedy (and very nice) websites without a lot of effort. If you happen to know some html and css you have the opportunity to expand on the website. If you don't know any and would like to learn how to, don't worry it is relatively easy to pick up the languages and even easier to configure (will be covered in a later post). 

Ideally, at some point I would like to have my own server to run my website on. But for now as a free alternative this is really good. Let's talk about how to set it up.

## Setting up your GitHub Page
In order to create a GitHub page, you need to first create a new repository. GitHub pages allows you to create either a personal website/blog or a peroject website. The subtle difference between the two directly links to the url that is associated with your website. For example: 

```
https://[username].github.io/			# Personal website
https://[username].github.io/[repository] 	# Project website
```

To get the personal website url, name the repository `[username].github.io`. If you are interested in the project website, name it whatever you'd like.

To enable the repository as a website, go to the repo settings in your repository page, scroll down to the section labeled "GitHub Pages", on the drop down menu labeled "Source" either select master or whatever other branch you want to use to build the website. For the purpose of this post, we are going to stick with GitHub looking at the master branch to build. Your repository is now ready to be used as a website! Now to set up Jekyll.

## Installing Jekyll
The bulk of this section comes from the [Jekyll Docs Page](https://jekyllrb.com/docs/). In order to install Jekyll you need ruby, gcc, and make.

### Installing Ruby
To install ruby run: 

``` bash
sudo pacman -S ruby base-devel 					# Arch/Manjaro
sudo dnf install ruby ruby-devel @development-tools 		# Fedora
sudo apt-get install ruby-full build-essential			# Debian 
sudo zypper install -t pattern devel_ruby devel_C_C++		# OpenSUSE
sudo apt-get install ruby-full build-essential zlib1g-dev	# Ubuntu 
```

Now that it is installed, we to set up the ruby environment (adding paths and stuff like you would with Python). The [installation guide](https://jekyllrb.com/docs/installation/ubuntu/) suggests: 

``` bash
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

You can change it how you want, but if you run the commands above your environment should configured. To install Jekyll run:

``` bash
gem install jekyll bundler
```

## Setting Up Jekyll
Now that we have the GitHub repository and Jekyll installed, we can actually create the website. If you just want to make sure it is working (or just want to use the Minima theme), first clone the git repository you made, navigate into that directory and run:

``` bash
jekyll new myblog	# Places the content of the website in myblog 
jekyll new .		# Places the content of the website in the current directory
```

If you want to have another theme, the Jekyll website links some alterative options: 
1. [jamstackthemes.dev](jamstackthemes.dev)
2. [jekyllthemes.org](jekyllthemes.org)
3. [jekyllthemes.io](jekyllthemes.io)

To install these, simply clone the repository into the directory you previously made.

### Running the Website Locally
If you want to make any edits or changes that you don't want to push to the internet, but would like to see what it would look like, you can run a local web server that lets you do just this! In the terminal, navigate to the directory that contains your webiste and run: 

``` bash
bundle exec jekyll serve
```

On you browser, load the url `http://localhost:4000` and you should see your website. 

### \_config.yml
This configuration file is what sets the title, description, url, base url, markdown, etc. In short it sets up a lot of things. The essentials are: 

``` yml
title: Your awesome title
author: GitHub User
email: your-email@domain.com
description: > # this means to ignore newlines until "show_excerpts:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
show_excerpts: false # set to true to show excerpts on the homepage

# Minima date format
# refer to https://shopify.github.io/liquid/filters/date/ if you want to customize this
minima:
  date_format: "%b %-d, %Y"

  # generate social links in footer
  social_links:
    twitter: jekyllrb
    github:  jekyll
    rss: rss
    # dribbble: jekyll
    # facebook: jekyll
    # flickr:   jekyll
    # instagram: jekyll
    # linkedin: jekyll
    # pinterest: jekyll
    # youtube: jekyll
    # youtube_channel: UC8CXR0-3I70i1tfPg1PAE1g
    # youtube_channel_name: CloudCannon
    # telegram: jekyll
    # googleplus: +jekyll
    # microdotblog: jekyll
    # keybase: jekyll

    # Mastodon instances
    # mastodon:
    # - username: jekyll
    #   instance: example.com
    # - username: jekyll2
    #   instance: example.com

# If you want to link only specific pages in your header, uncomment
# this and add the path to the pages in order as they should show up
#header_pages:
# - about.md

# Build settings
theme: minima

plugins:
 - jekyll-feed
 - jekyll-seo-tag
```

This is copied from the Minima theme. Everything is pretty self explanitory. The only thing that got me initially was setting the url. If you are running a personal page you need to add the line:

``` yml
title: Your awesome title
author: GitHub User
url: 'https://[username].github.io' # <-----
email: your-email@domain.com
```

If you have a project website you need to add: 

``` yml
title: Your awesome title
author: GitHub User
url: 'https://[username].github.io' # <-----
baseurl: '/[repository name]' # <----
email: your-email@domain.com
```

If you push all these changes to your repository, you should have a working website!

## Sources
* [GitHub Pages Website](https://pages.github.com/)
* [Jekyll Home Page](https://jekyllrb.com/)
* [Minima](https://github.com/jekyll/minima)
