+++
title = "Deploy your HUGO website online"

date = 2018-10-20T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
linktitle = "deploy website"
[menu.tutorial]
  parent = "HUGO"
  weight = 2

# Featured image.
# Uncomment below lines to use.
#[header]
#  image = "headers/hugo.png"
#  caption = "Image credit: [**HUGO**](https:https://gohugo.io)"

+++

# Deploy on Netlify

## steps
Deploy your HUGO website on Netlify is astonishingly easy, if you are a beginner, it is recommended to use this approach.  

Netlify is free and provides fast global access, automated deployment when you add or modify content, and one-click HTTPS security. Netlify free account will create a non-sense domain for your website, to deploy, simply:  

* Create a [Netlify account](https://www.netlify.com)
* create a repository on Github(Netlify also support other providers)for you finished website
* Log-in Netlify and then click **New site from git** and follow click-and-confirm instructions from Netlify
* Wait a couple minutes, and you are good to go.


# Deploy on GitHub Pages

Acknowledgement: This post is a direct reproduction of [whipperstacker's blog][1]. 
  
I found it extremely useful when it comes to deploy your Hugo sites on Github pages. It nails it perfectly!

---

## Let's get Started!
If you already know how to use Hugo, and you've never used GitHub Pages before, and
you just want to figure out how to get everything wired up and deployed with the least
amount of fuss necessary, then a lot of the blog posts and tutorials you'll find are
going to be a bit frustrating.

Some tutorials will explain the GitHub Pages part in detail, but will make assumptions
about how you're generating your site, which won't necessarily match what Hugo does.

Other tutorials will assume that you know _nothing_, and will explain every step of
everything from scratch.

This post assumes that you know what all the pieces are (hugo, repositories, a bit of DNS),
and you just want to figure out the easiest way to stitch it all together.

First, a warning:

## Don't Make a `gh-pages` Branch

A lot of the documentation you'll find will talk about creating a branch
called `gh-pages` for the HTML. This is great if you're creating a portfolio
site with sub-sites for different projects on GitHub.

If you're looking to create a stand-alone site mapped to a custom domain,
then that is not the documentation you need.

The `gh-pages` branches are what GitHub refers to as _Project Pages_. What
you need when creating a stand-alone site are _User Pages_ or _Organization Pages_
(which are the same thing, it just depends on if your GitHub user is a user
or an organization).

Ok, moving on.

## A Tale of Two Repositories

The trick to deploying a stand-alone, hugo-generated site that will be hosted
on a custom domain is that everything within `public/` needs to be in its own
repository, and that repository _must_ be named `<username>.github.io`, where
`<username>` is your actual GitHub username.

This means that all the markdown and templates and configuration needs to go in
a separate repository. The repository with all the Hugo stuff can be named
whatever you like. For the sake of argument, let's assume this repository is called `blog`.

The initial setup depends on what your current situation is. Most likely, either:

1. nothing is committed to source control yet, or
1. you already have your hugo site committed and pushed up to the `blog` repository
   on GitHub.

### Setup When Nothing is Committed(select one of this two)

Create two new, empty repositories on GitHub:

1. `blog`
1. `<username>.github.io` Make sure to check the *Initialize this repository with a
   README* box, since that will make the next step easier.

Kill your hugo server so that it stops regenerating the HTML.

Delete the `public/` directory with `rm -r public/`.

Initialize a git repository and add the remote:

    $ git init
    $ git remote add origin git@github.com:<username>/blog.git

### Setup When You've Already Committed and Pushed(select one of this two)

If you've already got your Hugo site committed to source control and pushed up to
GitHub, then the process is similar, except that you need to make room for the submodule
that you're going to add right after the setup is complete.

Kill your hugo server so that it stops regenerating the HTML.

Create a new, empty repository named `<username>.github.io` on GitHub, making sure
to tick the *Initialize this repository with a README* box.

Delete the `public/` directory from git:

    $ git rm -r public

### Adding the Submodule

Clone the `<username>.github.io` repo into a submodule in `public`:

    $ git submodule add git@github.com:<username>/<username>.github.io.git public

Add everything and push it up to GitHub:

    $ git add .
    $ git push -u origin master

### Deploying

Regenerate the HTML and push the submodule up to GitHub:

    $ hugo -t -theme=YOURTHEME
    $ cd public
    $ git add .
    $ git commit -m "Generate site"
    $ git push origin master

You should be able to see the index page up on <username>.github.io a few moments later.

Add a handy deploy script like [Spencer Lyon's script][deploy] to simplify things a bit.

### Make the whole deploying-procedure a shell script
```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo -t cocoa-eh # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```
Save the above content to a file like `deploy.sh`. And when you build your site to remote site, call `sh deploy.sh` and git add, commit and push if you also want to commit the changes of your site source files. 
## Mapping a Custom Domain

Whether you're going to use a subdomain like `blog.yoursite.com` or an apex domain like
`yoursite.com`, you need to first add a file named CNAME to the submodule repository containing
the domain you're mapping to.

Note that this file should be named `CNAME`, even if the DNS record you're creating is an A record
or ALIAS record rather than a CNAME record.

If you're mapping a subdomain, create a CNAME record with your DNS provider. For an apex domain
you'll need either an ALIAS record on an A record. It depends on the provider.

For more information about DNS mappings, check out the [guide on GitHub][dns].

## Regenerating All the URLS

Once the DNS has propagated you're going to need to change the base host name in the Hugo config
file, regenerate the site with the correct urls, and redeploy.

[1]: https://github.com/whipperstacker/blog
[hugo]: http://gohugo.io/
[deploy]: https://github.com/spencerlyon2/hugo_gh_blog/blob/master/deploy.sh
[dns]: https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/

