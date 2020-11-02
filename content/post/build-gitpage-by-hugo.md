+++
date = "2020-02-08T22:07:46+08:00"
title = "Build Github webpage by Hugo"
draft = false
tags = ["Website","Github","Hugo"]
share = true
+++

## Overview

Github offers users a space to build personal pages. Their initial intention is to encourage users recording and sharing their works on Github so as to make the community thriving. While it should be static site hosting which means a front-end page without connections to backend, one could easily and fast initialize a personal website by build-in template, user-defined projects or static site generators such as Hugo and jekyll. I will focus on Hugo in this article. Besides, Hugo is the best choice if you are as lazy as me who prefer not spending too much time on coding for HTML, CSS and Javascript. You can build your site not longer than an hour. In the following, I will share how I did for building my site although there are several ways.

## Download and Install Hugo

Because my laptop is running with OS Windows 10 which does not have built-in package manager, I applied "Chocolatey" to install Hugo. With the software, we can easily enter the following command in terminal.
```
choco  install  hugo
```
For more detail, please visit the website [https://chocolatey.org/](https://chocolatey.org/).
The installation can be checked by the command
```
hugo version
```

## Create a blog project
Prior to starting this step, we should redirect the path to a directory where we hope to store the blog folder. Next, execute the following command.
```
hugo new site blog
```
Replace "blog" in the end of the command with any other desired name.
Finally, a message of success should be printed out in the terminal. We can in further check the directory with the name "blog" or the name you use in which the structure is like below.

```
.root/blog
+-- archetypes
|	+-- default.md
+-- config.toml
+-- content
+-- data
+-- layouts
+-- static
+-- themes
...
```
We will go over each files and folders in the following sections.

## Install a theme for your blog
While it is allowed to write your own theme or customize the style adapted from others' theme, we only introduce the procedure for building a personal page with templates provided in here [https://themes.gohugo.io/](https://themes.gohugo.io/).

In my site, I applied the template theme written by @[vjeantet](https://github.com/vjeantet/hugo-theme-casper/commits?author=vjeantet). To install the template, we can execute the command
```
cd blog/themes
git clone https://github.com/vjeantet/hugo-theme-casper
``` 

## Customize theme
Now, we have a template but we need to edit the `config.toml` for showing the content we want. Here is the example I used for my blog:

```
baseurl = "https://dwgoblue.github.io/"
languageCode = "en-us"
title = "DW Blog"
theme = "casper"
paginate = 2
Copyright = "© All rights reserved - 2020"
canonifyurls = true

[params]
description = "A scientist who loves to challenge himself."
authorlocation = "Ann Arbor, MI, USA"
cover = "images/cover.jpg"
author = "Da-Wei Lin"
bio= "Bioinformatics PhD student|University of Michigan, Ann Arbor"
logo = "images/signature.png"
githubName = "dwgoblue"
twitterName = "DaWeiLin4"
linkedinName = "da-wei-lin-331006197"
email = "daweilin@umich.edu"
instagramName = "daweilin"
hideHUGOSupport = false

[[menu.main]]  # here are the buttons on the menu
  name = "Home" # Button will display as "Home"
  weight = 100 # the weight decides the position of the button (higher or lower)
  identifier = "home"
  pre = "<br />"
  url = "/"

[[menu.main]]
  name = "Blog"
  identifier = "blog" # this page will refer to a markdown file named "blog" in the content folder
  url = "/post"
  weight = 40

[[menu.main]]
  name = "About me"
  weight = -100
  identifier = "about"
  url = "/about"
  
[sitemap]
  ChangeFreq = ""
  Filename = "sitemap.xml"
  Priority = "-1"
```
Now, we are able to create a new blog article with the command
```
cd content/post
hugo new blog1.md
```
However, we are not sure how the layout looks like. To visualize the result, we could run the command

```
cd blog
hugo server
```
It would respond with the messages like below.
```
Building sites … WARN 2020/07/24 11:45:34 Page's .URL is deprecated and will be removed in a future release. Use .Permalink or .RelPermalink. If what you want is the front matter URL value, use .Params.url.
WARN 2020/07/24 11:45:34 Page's .RSSLink is deprecated and will be removed in a future release. Use the Output Format's link, e.g. something like:
    {{ with .OutputFormats.Get "RSS" }}{{ .RelPermalink }}{{ end }}.
WARN 2020/07/24 11:45:34 Page's .Hugo is deprecated and will be removed in a future release. Use the global hugo function.

                   | EN
+------------------+----+
  Pages            | 17
  Paginator pages  |  1
  Non-page files   |  0
  Static files     | 26
  Processed images |  0
  Aliases          |  7
  Sitemaps         |  1
  Cleaned          |  0

Total in 392 ms
Watching for changes in C:\Users\lynch\DWblog\{content,data,layouts,static,themes}
Watching for config changes in C:\Users\lynch\DWblog\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

## Deploy onto Gitpage
There are two ways to complete this step. Firstly, we can directly create a `public` folder for publishing our blog with `hugo` command. It is followed by pushing the `public` folder onto Gitpage repo.

```
cd blog
hugo
cd public
git init  
git add .  
git remote add origin [https://github.com/username/username.github.io.git](https://github.com/username/username.github.io.git)  
git commit -m “first commit”  
git push origin master
```
Apparently, we should create a repo for storing those contents. Note that we have to initiate the repo with a name as `username.github.io` without `README.md`. Then, we should be able to see your blog when visiting the url https://github.com/username/username.github.io.git.

However, this way requires to push blog content and the public content respectively. According to Hugo official instruction, we are able to create a submodule in our blog folder before using `hugo` command to add `public` folder.
1. Create a new repo with a name as `username.github.io` without `README.md`. 
2. Clone the repo to local space and change the working directory into the folder with `cd`.
3. Copy and paste all the content from your blog folder into the working directory.
4. Run `rm -rf public` for killing previously existed `public` folder (optional).
5. Create a submodule by `git submodule add -b master https://github.com/<USERNAME>/<USERNAME>.github.io.git public`.
6. Run `hugo` command to create `public`.
7. To save time in the future, we can write a `deploy.sh` script for fast pushing (visit Hugo official instruction for more detail).

## Summary
Hugo is easy-to-use for people who are not interested in spending a lot of time on CSS, HTML and so on. Instead, one can easily start a blog on Gitpage less than 30 minutes and simply focus on the content of blog articles with markdown language. Therefore, use Hugo if you are as lazy as me!!!

## Reference

 - Build a Personal Website With Github Pages and Hugo [https://levelup.gitconnected.com/build-a-personal-website-with-github-pages-and-hugo-6c68592204c7](https://levelup.gitconnected.com/build-a-personal-website-with-github-pages-and-hugo-6c68592204c7)
 - Host on GitHub [https://gohugo.io/hosting-and-deployment/hosting-on-github/](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
 - CASPER theme for hugo [https://github.com/vjeantet/hugo-theme-casper](https://github.com/vjeantet/hugo-theme-casper)
