---
layout: page
root: ..
title: Karl notes for git tutorial
---


### Why use git?

- Keep track of entire history of code
- Easy to explore that history
- Investigate the state of things at any particular time
  - Suppose you just realized your script isn't working any more
  - What happened? When?
- Collaborate on analysis projects
  - Merge simultaneous changes
- Github
  - Easy collaboration
  - [Contribute to the community](https://github.com/hadley/ggplot2/pull/1089)


### Pains in git

- Written by and for very savvy programmers
- Almost useless error messages
- manuals amusingly bad (See the [git man page generator](http://git-man-page-generator.lokaltog.net/))


### Explore GitHub repositories

- Big:
  - [ggplot2](github.com/hadley/ggplot2)
  - [dplyr](https://github.com/hadley/dplyr)
  - [R/qtl](https://github.com/kbroman/qtl)
- Small
  - `~/Projects/FuadSurv`
  - [`ProgrammingNotes`](https://github.com/kbroman/ProgrammingNotes)
  - [`FruitSnacks`](https://github.com/kbroman/FruitSnacks)



### Setting Up

The first time we use Git on a new machine,
we need to configure a few things.
Here's how Dracula sets up his new laptop:

~~~ {.bash}
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
$ git config --global color.ui "auto"
$ git config --global core.editor "nano"
~~~

Git commands are written `git verb`,
where `verb` is what we actually want it to do.
In this case,
we're telling Git:

*   our name and email address,
*   to colorize output,
*   what our favorite text editor is, and
*   that we want to use these settings globally (i.e., for every project),

The four commands above only need to be run once:
the flag `--global` tells Git to use the settings for every project on this machine.

The commands modify the file `~/.gitconfig`. Type `less ~/.gitconfig`
(or `cat ~/.gitconfig`) to see what they did.


### Creating a Repository

~~~ {.bash}
$ mkdir my_new_project
$ cd my_new_project
$ git init
~~~


~~~ {.bash}
$ cd ~/Desktop/SWC_2015-04-27
$ git init
~~~

**Whenever you start a new project**, your first thought should be "`git init`".


~~~ {.bash}
$ ls -A
$ ls -A .git
~~~


~~~ {.bash}
$ git status
~~~

### Key commands

- `git config`
- `git init`

- `git status`
- `git diff`
- `git log`

- `git add`
- `git commit`


### Play with that fresh repository

- Add a ReadMe file
- status
- add
- status
- commit
- status
- log
- add some more text
- status
- add
- status
- commit

### How to get rid of the whole git repository thing

- `rm -rf .git`



### Add files from yesterday

~~~ {.bash}
$ git add R/*.R
$ git status
$ git add data/gapminder.csv
$ git status
$ git commit -m "Initial commit"
~~~


### Start a new script

- First, create an R file and add an outline
  - Load data and packages
  - Five countries with lowest lifeExp in 1952
  - Five countries with highest lifeExp in 1952
  - Five countries with lowest lifeExp in 2007
  - Five countries with highest lifeExp in 2007
  - Plot data for these groups
- Second, add code for 5 lowest and 5 highest in 1952
- Third, add code for...
- Fourth, plot over time


~~~ {.r}
gapminder %>%
    filter(year==1952) %>%
    arrange(lifeExp) %>%
    select(country) %>%
    head(5)
~~~


### Commits

- What to commit (and what not to commit)?
- How often to commit?
- What should the commit messages be like?



### Why the add/commit separation?


### Looking at the history with `git log`


~~~ {.bash}
$ git log
$ git log --stat
$ git log -3 --stat
$ git log -3 --oneline
~~~


### Changes to a file with `git diff`

~~~ {.bash}
$ git diff
$ git diff --staged
$ git diff blah.txt
$ git diff HEAD~1 blah.R
$ git diff HEAD~2 blah.R
$ git diff --stat
~~~


### Fixing things

- unstaging files
- fix that last commit message
- dump these changes
- checkout some previous state






### Ignoring Things

~~~ {.bash}
nano .gitignore
~~~


### Notes on R stuff

~~~ {.r}
gapminder <- read.csv("data/gapminder")
library(dplyr)
library(ggplot2)

lo1952 <- gapminder %>%
              filter(year==1952) %>%
              arrange(lifeExp) %>%
              head(5)

hi1952 <- gapminder %>%
              filter(year==1952) %>%
              arrange(lifeExp) %>%
              tail(5)

lo2007 <- gapminder %>%
              filter(year==2007) %>%
              arrange(lifeExp) %>%
              head(5)

hi2007 <- gapminder %>%
              filter(year==2007) %>%
              arrange(lifeExp) %>%
              tail(5)

of_interest <- rbind(lo1952, lo2007, hi1952, hi2007)$country %>% unique

gapminder %>%
    filter(country %in% of_interest) %>%
    ggplot(aes(x=year, y=lifeExp, group=country)) +
    geom_line() +
    facet_wrap(~country)

ave_lifeExp <- gapminder %>%
                   group_by(country) %>%
                   summarize(ave_lifeExp=mean(lifeExp)) %>%
                   arrange(ave_lifeExp)

gapminder_ro <- gapminder
gapminder_ro$country <- factor(gapminder$country, levels=ave_lifeExp$country)

gapminder_ro %>%
    filter(country %in% of_interest) %>%
    ggplot(aes(x=year, y=lifeExp, group=country)) +
    geom_line() +
    facet_wrap(~country)
~~~
