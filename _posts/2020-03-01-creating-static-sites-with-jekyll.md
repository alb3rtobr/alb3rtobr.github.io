---
title: "Creating static sites with Jekyll"
date: 2020-03-01 01:00:00 +0800
categories: [Blogging]
tags: [Jekyll]
toc: false
---

Jekyll is a static site generator, written in Ruby, that allows you to create sites like this blog using Markdown language.
When deciding how to create a new blog, I had different alternatives (wordpress, medium...) but I decided to use Jekyll for several reasons:
* Use Markdown to write posts. I already use it to take personal notes, so it will be easier to transform some of them on new posts.
* As GitHub uses it as the system behind GitHub Pages, I can have a hosted site for free.
* Good excuse to learn Ruby if needed.

![Jekyll logo]({{ "/assets/img/jekyll_logo.png" | relative_url }})

Although thanks to Docker, its not even necessary to install Ruby to create a site with Jekyll.
There are some good guides about Jekyll, so I will just summarize what I did:
* Find a theme. I selected one called [chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/).
* Fork the theme repository, and rename it to 'alb3rtobr.github.io'.
* Personalize the theme modifying `_config.yml`.
* Write this first post :)

Using the [official Jekyll Docker image](https://hub.docker.com/r/jekyll/jekyll/) it is possible to build the site locally before committing any change to the repo.

First, to build the site (this step is only needed for creating the site locally):

```console
$ docker run --rm --volume="$PWD:/srv/jekyll" -it jekyll/jekyll:3.8 jekyll build
```

And after that, to serve the site:

```console
$ docker run --volume="$PWD:/srv/jekyll" -p 3000:4000 -it jekyll/jekyll:3.8 jekyll serve --watch --drafts
```
Running this command the site will be available at `localhost:3000`.

## Links:

* [Jekyll official site](https://https://jekyllrb.com/)
* [Jekyll's GitHub repository](https://github.com/jekyll/jekyll)
* [jekyllthemes.org](http://jekyllthemes.org/)
* [GitHub Pages](https://pages.github.com/)
* [Running Jekyll in Docker](https://ddewaele.github.io/running-jekyll-in-docker/) (tutorial)
