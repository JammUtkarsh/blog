---
title: 3 Ways Containers Changed My Life
date: 2022-06-12
tags: [docker, containers, linux, productivity]
---

![Cover](/images/1_cover.png)

My goal with this article is to motivate you to try a new technology or maybe even use it in a more personal way than the usual 'this will get me a job' way.

## **The Story**

One of the steps to becoming a 'DevOps Engineer' is to be comfortable with GNU/Linux. [Docker](https://www.docker.com/) is one such platform that makes accessibility to this tool easier, even in your native OS like Windows. The containerization technology as a whole solved a lot of problems. For me, it has improved the way I organize my files, programs, and software, and overall the way I work. Less clutter (at least I experienced it).

I liked the methodology **so much** that I formatted my Mac, and

<blockquote class="twitter-tweet" data-theme="light"><p lang="en" dir="ltr">Now my laptop is full of containers and images rather than packages. 😶</p>&mdash; Utkarsh (@JammUtkarsh) <a href="https://twitter.com/JammUtkarsh/status/1463160276828700685?ref_src=twsrc%5Etfw">November 23, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## Let's Get Started

Side Note: *I am going to use the word **'package'** for development kits like Go, Python, JDK, etc.*

### 1. Install and track

The very first thing to learn about any programming language or piece of software is to install it.
Here are the minimum number of steps you would need to follow:

- Visit the website.
- Download and run the package installer.
- Get started with coding.

![Normal Method](/images/1_normalMethod.png)

This is a long, time-consuming process, especially during installation if you are on a slow laptop. Plus, it comes with some baggage:

1. Track the packages you have installed.
2. Search 'how to uninstall package X?' *(because every package has a different method and is sometimes difficult too)* and make sure there are no files left in my **limited storage** space.

With Docker, it's as easy as:

- Open terminal
- Run a container.
- `ssh` into the container
- Start your development *(in vim to stay in terminal forever)*.

![Docker Method](/images/1_dockerMethod.png)

Not to mention, I am doing this with just a terminal and with what is sometimes called a container register like [hub.docker.com](http://hub.docker.com/) Now,

1. `docker image ls` and here is the list of images or SDK installed.
2. `docker image rm ${name_of_image}` and it's gone.
3. It usually takes less space if the right one is chosen *(alpine or slim)*.

### 2. Possibility of software interference or breaking changes

This might be a small issue; possibly you or I will never encounter it, but now you have a package installed on your machine that can cause some dependency issues with other packages or software. That would be troublesome.

The best real-life example that I can think of is in Python. `brew install python@3` and boom, I have python3 installed, but there is a program that runs on python2. So I have to install or maybe revert to the default `python@2`. This could be annoying. On switching the project, which uses Python 3, I run `python main.py`, and it throws an error or something because of the version difference.

When developing in a container, you are sandboxed into that environment. Doesn't affect anything outside that environment. Allowing us to focus on application development and getting out of 'setting up development environments" loop.

### 3. Learning GNU/Linux

I think you become a better developer once you start using Linux. This is especially true for students or newbie developers. You become better at debugging and problem-solving. There are just too many benefits to having Linux in your arsenal.

The best way to get your hands dirty is to start using it. But the question is, where do I find the dirt to play with?

Earlier, I would have recommended something like

- Using WSL/WSL2 for Windows *(Moderate Difficulty)*
- Setting up a VM *(Fairly difficult and complex.
- Installing Linux as your main OS *(Fairly hard and complex)*.
- Using the cloud *(Expensive and complicated.

All these come with their own level of difficulty and challenge, which might be fun if you are interested in exploring your options.

In my opinion, Docker is the easiest to recommend because:

1. Easy to install
2. Easy to manage
3. You could give predefined commands to start working in the shell of the container).
4. Accessibility to various Linux environments

## Hold up

Ultimately, containers were designed to solve a specific problem. As an *Indian*, I discovered ways to use it for my own purposes as well. There are or will be some downsides to using containers for the things I mentioned above.

1. **No GUI interaction**: You will only be learning Linux in the shell (though that's where you will be working in production).
2. **Bandwidth Consumption**: downloading a Docker image and running VS Code in the container consumes a lot of bandwidth. When there is no internet, even if you have an image downloaded, you can't open and run it on an IDE. But there is always a workaround. **Vim**
3. **Processing Power**: You do need a good workstation to run Docker, especially if you are a Windows or macOS user. It consumes a significant amount of power, memory, and CPU. That's because Docker needs to run a Linux VM first.

## Conclusion

Docker and Linux are just tools, just like a knife and a samurai sword. You want to cut the veggies with a knife or a samurai sword; it totally depends on you. One might make you look cooler, while the other might make you more effective.

If you are starting out, get as many veggie cutters as you want. Try them. Keep some in your drawer and others in the basement. Who knows when you might need to use them?

Ultimately, with experience, you know the pros and cons of each tool. You will eventually possess the knowledge of 'what to use in X situation.

---
