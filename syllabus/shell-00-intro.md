---
layout: page
Title: The Unix Shell
---

## Initial setup (for Windows users only):

Open your Terminal and type the following command:

```
echo "export TERM=msys" >> ~/.bashrc
```

then restart your machine.

## What is the shell and how do I access it?

The *shell* is a program that presents a command line interface which allows you to control your computer using commands entered with a keyboard instead of controlling graphical user interfaces (GUIs) with a mouse/keyboard combination.

A *terminal* is a program you run that gives you access to the shell. There are many different terminal programs that vary across operating systems.

Some important reasons to learn about the shell:

1.  It is very common to encounter the shell and command-line-interfaces in scientific computing, so you will probably have to learn it eventually;

2.  The shell is a really powerful way of interacting with your computer. GUIs and the shell are complementary - by knowing both you will greatly expand the range of tasks you can accomplish with your computer. You will also be able to perform many tasks more efficiently;

3.	More reasons: access remote servers, repeatability, documentation.

The shell is just a program and there are many different shell programs that have been developed. The most common shell (and the one we will use) is called the Bourne-Again SHell (bash). Even if bash is not the default shell, it is usually installed on most systems and can be started by typing `bash` in the terminal. Many commands, especially a lot of the basic ones, work across the various shells but many things are different. I recommend sticking with bash and learning it well. ([Here is a link for more information](http://en.wikipedia.org/wiki/Bash_%28Unix_shell%29))

***

Acknowledgments: these lessons were adapted by Kara Woo from materials by [Diego Barneche](http://nicercode.github.io/2014-02-13-UNSW/lessons/60-shell/).
