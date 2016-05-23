# ernest.io

The ernest.io site is based on the [Hugo Bootstrap Premium theme](https://github.com/appernetic/hugo-bootstrap-premium), and takes inspiration from the [nats.io site](http://nats.io).

## Contributing Content

We view this project as a perpetual work in progress that can greatly benefit from and be enriched by the knowledge, wisdom and experience of our community.

We follow the standard Fork-and-Branch GitHub workflow. If you're not familiar with this process, please refer to either of the following excellent guides:

* ['Forking Projects' GitHub Guide](https://guides.github.com/activities/forking/)

* ['Fork a Repo' GitHub Help article](https://help.github.com/articles/fork-a-repo/)

We encourage and welcome your contributions to any part or element of this site. We will review and discuss with you any contributions or corrections submitted via GitHub Pull Request.

## Checking Your Work

To make sure your changes render correctly, you can build and preview the site on your local system using Hugo. 

**Note 1:** On OS X, if you have [Homebrew](http://brew.sh/), installation is even easier: just run brew install hugo.

**Note 2:** Hugo requires Go 1.4+. If Go is not already installed on your system, you can [get it here](https://golang.org/dl/).

Now install Hugo:

```
go get -u -v github.com/spf13/hugo
```

Clone your forked copy of the repository:

```
git clone git@github.com:<YOUR GIT USERNAME>/ernest-site.git
```

Change to the directory:

```
cd ernest-site/
```

Build the site and start the server:

```
hugo server -w
```

One great thing about Hugo is that it has a live preview mode. In live preview mode, Hugo spawns a web server that detects content updates in the tree and will render Markdown to HTML in real time. This means you can see the updated content and layout in real time as you edit!

