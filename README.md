# aerobless.github.io

My [personal github page](https://aerobless.github.io/) containing various side-projects, ideas or just random snippets of stuff that I find interesting. This is very much a raw / work in progress kinda thing. Visit at your own peril :)

# stack

This page is built using [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

+ **Install:** `docker pull squidfunk/mkdocs-material`
+ **Run locally:** `docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material`
+ **Publish:** `docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material gh-deploy`
