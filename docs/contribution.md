---
title: Contributing to the Wiki
layout: default
nav_order: 7
---

# Contributing to the Wiki

I personally had an issue with this myself, so this is for future contributors. I already fixed the gems file to use liquid 4.0.4 in the repository so it should work.

## Software perquisites
Here are some REQUIRED software perquisites if you want to build the website locally to see how it would look:
* [Git Bash](https://git-scm.com/downloads)
* [Jekyll](https://jekyllrb.com/docs/installation/)
  * When installing Ruby, be sure to use Option 3 `MSYS2 and MINGW development toolchain` in the RubyInstaller2 for Windows terminal that shows up. Run `ridk enable` in a **new** terminal window afterwards to activate MSYS2 tools on the command prompt.
  * This is the documentation I followed when first setting up the website: [GitHub - Test site locally with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

You might also have to install RVM manually, which is done with the following steps.
1. First step is to type / paste into Git Bash the following command: `gpg --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB` 
  * This is required to install RVM! If the security keys don't match, then you won't be able to install RVM.
2. After the keys are set, type `\curl -sSL https://get.rvm.io | bash -s stable --ruby` which installs RVM.

<details>

<summary>This may not apply anymore as the gem file has been configured by me to use liquid 4.0.4, but just in case you have to manually do all of this again...</summary>

You also have to install Liquid version 4.0.4 instead of 4.0.3, otherwise you will get an error that says something like `"undefined method: tainted"`. Now of course, this isn't exactly what was said, but this is what fixed it. The command to install v4.0.4 through Git Bash is below.
* `install liquid -v 4.0.4`

You may also need to install webrick, which can be done by typing:
* `bundle add webrick`

</details>

## Running the website locally
With all of that out of the way, be sure to reopen your terminal after installing all of that. Then, if everything is right all you need to do is set Git Bash to the cloned repository on your computer, then `bundle install`, then `bundle exec jekyll serve`. Here's how I did it as an example.

1. So, since I'm using GitHub Desktop, all cloned repositories are located in `E:\Documents\GitHub` and the cloned repository address is `E:\Documents\GitHub\FinalityMC-web`
  * In Git Bash I would have to type `cd /e/Documents/GitHub/FinalityMC-web` then press Enter. If the directory address shows up in yellow text in the next pending user input line, good.
2. Type `bundle install`
  * If Git Bash says it does not have permission to write, try running it in Administrator even though it is advised against. However, for the life of me I CANNOT FIGURE OUT HOW TO DO IT THE RECOMMENDED WAY so I just right clicked Git Bash and clicked `Run as administrator` to save myself some headache.
3. After it is done installing, type `bundle exec jekyll serve`
  * If everything goes right, the locally hosted URL will show up in the Git Bash terminal.

* Pass the `--livereload` option to serve to automatically refresh the page with each change you make to the source files: `bundle exec jekyll serve --livereload`

These are the same instructions as mentioned in the Jekyll docs here: [Jekyll - Quickstart](https://jekyllrb.com/docs/)

## Where do I write stuff?
So here's the cool part... EVERYTHING IS IN MARKDOWN! All the heavy lifting is done by everything else, all it needs is text.
* `index.md` is the homepage
* Everything in the `docs` folder is for everything else, including children pages. 