+++
date = "2018-10-31T08:48:23+01:00"
draft = false
title = "Free static site using Hugo and Github pages"
summary = "Guide to get you started with a free static webpage using Hugo and Github pages."
+++
# Free static site using Hugo and Github pages
------
This is a guide to get you started with a free static webpage using Hugo and Github pages. 
<br />
<br />
<br />
## Prerequisites
------
* Github account
* Git version 2.8 or higher
* Latest version of Hugo

Ubuntus repos for Hugo is maintained by Canonical and will provied you with an outdated version, therefore we will do this manually.

_Note: For the theme [Tale](https://github.com/EmielH/tale-hugo) we need the extended version of Hugo._

### Download the latest Hugo package
Start by downloading the latest hugo package `wget https://github.com/gohugoio/hugo/releases/download/v0.50/hugo_extended_0.50_Linux-64bit.deb`
 
Install the downloaded package `sudo dpkg -i hugo_extended_0.50_Linux-64bit.deb`. If the latest version isn't "0.50" just replace it with the latest version number.
<br />
<br />
<br />
## Setup
------
Create a repository on github.com to hold the source files, this is where you will be creating content, configure your site, add/edit posts, etc. Clone your repository and run the following commands.

Initiate a new site `hugo new site [sitename]`

Move files from [sitename] folder to the repository root `cp -a [sitename]/. .`

Add the [Tale](https://github.com/EmielH/tale-hugo) theme to your site.

`git submodule add https://github.com/EmielH/tale-hugo`

Tell Hugo to use the theme Tale `echo 'theme = "tale"' >> config.toml`
<br />
<br />
<br />
## Create a post
------
To create a new post run `hugo new posts/some-name.md`, the new post will be placed in the posts folder inside the content folder which is placed in the root.
<br />
<br />
<br />
## Run locally
------
To test your site locally we want to start a local server, we do this by running the following command `hugo server -t tale`.

 Note: If your some-name.md post have the 'draft = true' set it will not appear.
<br />
<br />
<br />
## Deploy
------
Create a new repository named [USERNAME].github.io, this is where your site will be hosted. In your respository where your hugo site is installed you can remove your public folder with `rm -rf public` and then add the submodule to your site repository with `git submodule add -f https://github.com/[USERNAME]/[USERNAME].github.io.git public`.

To build your site run `hugo -t tale`, where "tale" being the name of the theme. Navigate to your public folder, add all files, commit and push. 
<br />
<br />
<br />
