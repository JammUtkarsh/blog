---
title: "Beyond The Browser: Expanding Online Presence In Terminal"
tags: [markdown, terminal, glow, go]
date: 2023-06-24
---

## Introduction

![You](https://media.giphy.com/media/Ve7wX45gaOFmw8eeEM/giphy.gif)

must have some sort of online presence on the web. Right? It could be a GitHub account, a Leetcode profile, a place where you write blogs, or your portfolio website.
A common theme being followed here is that, they all need a web browser (*or a GUI*) to access them.

For some random reason (*or to look cool*), you should have a profile for **terminal** too. Of course, it doesn’t need to be an identical replica of what’s in the browser. It could be something on its own!

## IRL Examples

I have some magic ~~tricks~~ commands up my sleeve to show you!

Run

```bash
docker run --rm -it jammutkarsh/intro
```

To render my *About Me*

![Intro In Terminal](/images/4_Intro.png)

> Source code: <https://github.com/JammUtkarsh/jammutkarsh>

Run

```bash
docker run --rm -it jammutkarsh/blog
```

To read my blogs in terminal, **with scrolling** on!

![Blog GIF](/images/4_Blog.gif)

> Source code: <https://github.com/JammUtkarsh/blog>

Internally, it's running

## Glow + Markdown

You must have heard of [Markdown](https://www.markdownguide.org/), a *de facto* markup language, *simpler than HTML*, used in almost every other blogging or content (*like documentation*) **web**site.
Don’t trust me, [read here](https://www.markdownguide.org/getting-started/#whats-markdown-good-for)!

Frameworks like [Hexo](https://hexo.io/), React, or NextJS convert `.md` files into `.html` and possibly `.css` files depending upon their internal design to be rendered on web.

Similarly, [Glow](https://github.com/charmbracelet/glow) a command-line tool that is **free**, **open-source**, and **awesome** can render the `.md` files in the terminal.

The examples up there were internally using `glow`.

## Lighter Than A Container

I am using Docker, a very resource intensive tool to create the simple artwork. The same can be achieved using `glow` and a URL.

Try: `glow -p github.com/charmbracelet/glow` (*Pretty URL*)

So, if you have installed `glow` on your machine, you can render **any** raw markdown from **URL** with much **less** resources being used
Like run `glow -p https://raw.githubusercontent.com/JammUtkarsh/blog/main/source/_posts/terminal-inside.md` (*Ugly URL*) to render this blog.

> We are using -p flag to enable pager, which is similar to scrolling.

The **ugly** part of this approach is the **URL**. You need to have some sort of URL shortener or a tool which makes URL look friendlier.

## Conclusions

Apart from having a smooth **keyboard-only** experience, we are only limited to rendering text!

There are definitely a lot of libraries and tools that render audio, video, images, etc., but each comes with their own baggage That, IMO, is not practical for the end user to see some text!

> Tip: Read this blog in terminal, and you won't see the distracting GIFs!

---
