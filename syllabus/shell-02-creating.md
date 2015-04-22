---
layout: page
Title: Creating, moving, and deleting files and directories
---

# Creating, moving, and deleting files and directories

I'm going to be working mainly in the `Desktop` directory -- recommend that people follow along.

## Creating an empty file

Lets create an empty file using the `touch` command. Enter the command:

~~~
$ touch testfile
~~~
{:class="in"}

Then list the contents of the directory again using `ls`. You should see that a new entry, called `testfile`, exists. It does not have a slash at the end, showing that it is not a directory. The `touch` command just creates an empty file.

Some terminals can color the directory entries in this very convenient way. In those terminals, use `ls -G` instead of `ls` if you are on a Mac or `ls --color` if you run on Windows. Now your directories, files, and executables will have different colors.

Now if you use the command `ls -l` you will notice that `testfile` has a size of zero. OK then, let's get rid of `testfile`. To remove a file, just enter the command:

~~~
$ rm -i testfile
~~~
{:class="in"}

When prompted, type:

~~~
$ y
~~~
{:class="in"}

The `rm` command can be used to remove files. The `-i` adds the "are you sure?" message. If you enter `ls` again, you will see that `testfile` is gone.

***Warning: The shell does not have a recycling bin. So any file removed with `rm` is gone forever. Use with caution. Remember the -i argument***

If you want to create a file with some text, say notes about what you are doing, you'll need to use a text editor. The one we'll be using here is nano.

> #### Which Editor?
>
> When we say, "`nano` is a text editor," we really do mean "text": it can
> only work with plain character data, not tables, images, or any other
> human-friendly media. We use it in examples because almost anyone can
> drive it anywhere without training, but please use something more
> powerful for real work. On Unix systems (such as Linux and Mac OS X),
> many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
> [Vim](http://www.vim.org/) (both of which are completely unintuitive,
> even by Unix standards), or a graphical editor such as
> [Gedit](http://projects.gnome.org/gedit/). On Windows, you may wish to
> use [Notepad++](http://notepad-plus-plus.org/).
>
> No matter what editor you use, you will need to know where it searches
> for and saves files. If you start it from the shell, it will (probably)
> use your current working directory as its default location. If you use
> your computer's start menu, it may want to save files in your desktop or
> documents directory instead. You can change this by navigating to
> another directory the first time you "Save As..."

To create a new file and open nano, type

~~~
$ nano notes.txt
~~~
{:class="in"}

*Pause to make sure this worked for everyone, especially Windows users who may not have installed nano.*

Now, type a line of text, something like "This is where I am keeping my notes." To exit, hit Ctrl-X, then Y (to save), then Enter.

Now use `ls` to view the contents of your desktop. Do you see the file you created? *(Does anyone not see it?)*

**Exercise:** View the contents of the file you just created within your terminal (hint: we learned a command for viewing the contents of a file in the last section). Then, open the file, add some more text to it, save it, and exit.

## Manipulating the file system

Make directories with `mkdir`. This will create a new directory within the current directory.

~~~
$ mkdir software-carpentry
~~~
{:class="in"}

You can create as many folders as you like in a single call.

~~~
$ mkdir directory_name_1 directory_name_2 directory_name_3
~~~
{:class="in"}

To copy and move files, we use the commands `cp` and `mv`, followed by the file you want to copy/move, and then the location that you want to copy/move it to.

~~~
$ cp file1 file2
$ mv file1 file2
~~~
{:class="in"}

So if I am in my data directory and I want to copy or move one of the data files to my desktop, I would do. *(Do these, then show them on the Desktop. Do rm ~/Desktop/car-speeds.csv in between.)*

~~~
$ cp gapminder.csv software-carpentry/
$ mv gapminder.csv software-carpentry/
~~~
{:class="in"}

`cp` and `mv` can also rename files. If you want to rename a file in place, just do:

~~~
$ mv file_oldname file_newname
~~~
{:class="in"}

When we moved `gapminder.csv` to the `software-carpentry` folder, if we'd wanted to rename it at the same time we could have done:

~~~
$ cp gapminder.csv software-carpentry/gapminder-2.csv
~~~
{:class="in"}

Both `cp` and `mv` can be used with directories in addition to files.

See the `man` command to get help on options you can use with these commands.

Remove files with `rm`.

## Let's try out some of the commands above

First create a temporary directory on your desktop. *Ask for people to call out commands to make directory and navigate into it.*

~~~
$ cd ~/Desktop
$ mkdir scratchpad
$ cd scratchpad
~~~
{:class="in"}

Make a few directories inside `scratchpad`

~~~
$ mkdir dir1 dir2 dir3
$ cp ~/Desktop/swc-data/*.png .
~~~
{:class="in"}

Use `ls` to view the contents of the current directory. What just happened? *(Ask for a volunteer)*

This is our first introduction to wildcards, which I'm going to talk a bit more about later. The `*.png` is telling the computer to match anything that ends in `.png`, which in this case is all of the figures from Karl's ggplot2 lesson.

Now try and remove scratchpad.

~~~
rm scratchpad
~~~
{:class="in"}

What just happened? If you want to remove everything within scratchpad no matter what, you will need to add the `-r` argument to function `rm`

~~~
rm -r scratchpad
~~~
{:class="in"}

*Maybe skip the below since it won't work for Windows users*

You can also create an entire directory structure with a single call (unfortunately this shortcut does not work in GitBash). e.g.

~~~
cd
mkdir -p test_project/{R,data,output/{data,figures},doc}
ls test_project/
~~~
{:class="in"}

This will create a project called `test_project` with the following structure:

~~~
|-- R/
|-- data/
|-- output/
|-- |-- data/
|-- |-- figures/
|-- doc/
~~~
{:class="out"}

One could also create lots of subdirectories at once using curly brackets expansions.

~~~
mkdir temp
cd temp
ls
mkdir dir-{0..10}
ls
rm -r temp
~~~
{:class="in"}

> ### Challenge {.challenge}
>
> Using the shell, create a folder on your desktop for materials from this
> workshop that looks like this *(Draw on the board)*.

~~~
|-- software-carpentry/
|-- |-- data/
|-- |-- |-- (data here)
|-- |-- R/
|-- |-- |-- (R scripts here)
|-- |-- notes/
|-- |-- figures/
|-- |-- |-- (figures here)
~~~
{:class="out"}

Note that this will break read.csv in your R script *go to RStudio and demonstrate, then use relative paths to fix loading of data*

***
Acknowledgments: these lessons were adapted by Kara Woo from materials by [Diego Barneche](http://nicercode.github.io/2014-02-13-UNSW/lessons/60-shell/).
