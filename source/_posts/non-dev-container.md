---
title: 3 Ways Docker Changed My Life
date: 2022-06-12
tags: [docker, containers, linux, productivity]
---

![Cover](/images/1_cover.png)

My goal with this article is to motivate you to try a new technology or maybe use it in a more personal way(than the usual 'this will get me a job' way).
**Article TLDR;**

1. Much more organized.
2. Zero-breaking packages.
3. Testing and learning made easy.

## **The Story**

One of the steps to becoming a 'DevOps Engineer' is to be comfortable with GNU/Linux. [Docker](https://www.docker.com/) is one such platform which makes accessibility to this tool easier, even in your native OS like Windows. The containerization technology as a whole solved a few problems, or I should say improved the way I organized my files, programs, software, overall the way I worked. Less clutter (at least I experienced it).

I liked the methodology so much that I format my Mac, and

<blockquote class="twitter-tweet" data-theme="light"><p lang="en" dir="ltr">Now my laptop is full of containers and images rather than packages. 😶</p>&mdash; Utkarsh (@JammUtkarsh) <a href="https://twitter.com/JammUtkarsh/status/1463160276828700685?ref_src=twsrc%5Etfw">November 23, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

So let's get started 🏁🏁🏁
*Side Note: I am gonna use the word **'package'** for development kits like go, python, JDK, etc.*

### 1. Install and track

If you wanted to learn something, the very first thing you needed to do was to install its package.
Here is the step count of the process.

![Normal Method](/images/1_normalMethod.png)
This is one-long time-consuming process. Especially installation if you are on a slow laptop and here comes the baggage:

1. Now you would have to track of a package which you have installed
2. Search how to uninstall it *( because every package has a different method and is sometimes difficult too)* and make sure there are no files left in my limited storage space.

With Docker, it's as easy as:

![Docker Method](/images/1_dockerMethod.png)

Not to mention, I am doing this with just using a terminal and with sometimes called a container register like [hub.docker.com](http://hub.docker.com/) Now,

1. `docker image ls` and here is the list of images or SDK installed
2. `docker image rm ${name_of_image}` and it's gone.
3. Usually takes less space, if the right one is chosen.

### 2. Possibility of software breaking or interference

This might be a small issue, possibly you or I might never encounter it but now. Say you have a package installed on your machine which can intervene with other packages or software. That would be trouble some. You would need to do something to isolate this.

The best real-life example that I have  is in python. `brew install python@3` and boom I have python3 installed but there is a program that runs on python2. So I have to install and change the default python version.

This is annoying. What if I have a project in python3, and I run `python main.py`, and it throws an error or something.

### 3. Learning GNU/Linux

I advocate for every computer science student to learning Linux. The best way to do so, is by getting their hands dirty. After convincing one to understand, the question of where is the dirt?

Earlier, I would recommendation something like

- WSL/WSL2 for windows *(Medium Difficulty)*
- Using a VM *(Fairly Difficult)*
- Native Install *(Fairly Difficult)*
- Using Cloud *(Expensive and a little complex)*

All these come with their level of difficulty and challenge, which might be fun if you are interested or just 'don't want to learn Linux' pain.
Docker is easy to recommend because:

1. Easy to install
2. Easy to manage
3. You could give predefined commands to start working in shell(of the container).

## Hold up

Let's be real, there are some downsides to it

1. **No GUI interaction**: You will only be learning Linux in the shell (Although that's where you will be working in production).
2. **Bandwidth Consumption**: downloading a docker image and installing the remote server in VSCode consumes a lot of bandwidth. When there is no internet, even if you have an image downloaded, you can't open and run on an IDE. But there is always a workaround!
3. **Processing Power**: You do need a good workstation to run docker, especially if you are a Windows or macOS user. It which consumes a significant amount of power, memory, and CPU.

That's all from my side, see you in the next one 🚀!
