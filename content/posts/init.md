+++
date = "2018-10-31T08:48:23+01:00"
draft = false
title = "init"
summary = "Guide to get you started with a free static webpage using Hugo and Github pages."
+++
# Init

Guide to get you started with a free static webpage using Hugo and Github pages. 

## Prerequisites

* Github account
* Git version 2.8 or higher
* Latest version of Hugo

Ubuntus repos for Hugo is maintained by Canonical and will provied you with an outdated version, therefore we will do this manually.

_Note: For the theme [Tale](https://github.com/EmielH/tale-hugo) we need the extended version of Hugo._

### Download the latest Hugo package

`wget https://github.com/gohugoio/hugo/releases/download/v0.50/hugo_extended_0.50_Linux-64bit.deb`
 
Install the downloaded package `sudo dpkg -i hugo_extended_0.50_Linux-64bit.deb`. If the latest version isn't "0.50" just replace it with the latest version number.

## Setup

Create a repository on github.com to hold the source files, this is where you create content. Clone your repository and run the following commands.

Initiate a new site `hugo new site [sitename]`

Move files from [sitename] folder to the repository root `cp -a [sitename]/. .`

Add the [Tale](https://github.com/EmielH/tale-hugo) theme to your site.

`git submodule add https://github.com/EmielH/tale-hugo`

Tell Hugo to use the theme Tale `echo 'theme = "tale"' >> config.toml`

## Create a post

To create a new post run `hugo new posts/some-name.md`

## Run locally

To start a local server with your theme run `hugo server -t tale`

_Note: If your some-name.md post have the 'draft = true' set it will not appear._
