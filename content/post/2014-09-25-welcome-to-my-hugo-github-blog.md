+++
date = "2014-09-25"
title = "My Hugo blog on GitHub pages"
description = "Setting up my Hugo generated blog and deploying on GitHub"
keywords = ["blog", "github", "hugo", "deployment"]
categories = ["blog"]
+++
This post opens my new shiny blog, where I write notes about creative technological fun on my experiments with electronics, 3d printing and computer programming.

The blog uses [Hugo](http://gohugo.io) static website generator and is deployed on [GitHub Pages](https://pages.github.com).
I hope you enjoy it; meanwhile here are some notes about the procedure I used to set it up and to deploy it.

---

### Setting up my blog

Create username.github.io repository on GitHub and clone the repository with

``` bash
git clone git@github.com:username/username.github.io.git
```

Create a branch where the files for Hugo to process are stored:

``` bash
git checkout --orphan source
```

We don't need a readme file on source branch:

``` bash
git rm README.md
```

As Hugo doesn't let you generate a new site in a directory where there are already files, generate the site skelethon in another directory with:

``` bash
hugo new site dirname
```

and move files to local git repository username.github.io;.

Commit what we have done so far:

``` bash
git add .
git commit -m "hugo skelethon"
```

Add a theme as a git subtree, but first give it a name as remote repository:

``` bash
git remote add -f hyde-my https://github.com/spf13/hyde.git
git subtree add --prefix themes/hyde hyde-my master --squash
```

Edit blog content and commit, then push the source branch to github:

``` bash
git push -u origin source
```

Generate the website and switch to master branch where the generated page should be stored

``` bash
hugo -t hyde-yv
git checkout master
```

Copy contents of public directory in root github repo, add files, commit and push to github.

Now the website should be online.
