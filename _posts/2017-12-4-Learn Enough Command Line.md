---
layout: post
title: "Learn Enough Command Line to Be Dangerous"
date: 2017-12-4
tags:
  Learn_Enou
  gh
  教材
  Command_Line
---
![cover](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ug92xfyj30fg0n80to.jpg)

# Learn Enough Command Line to Be Dangerous

**Michael Hartl**

A tutorial introduction to the Unix command line



*Learn Enough Command Line to Be Dangerous* is an introduction to the command line for complete beginners, the first in a [series of tutorials](http://learnenough.com/) designed to teach the common foundations of “computer magic” ([Box 1](https://www.learnenough.com/command-line-tutorial#aside-computer_magic)) to as broad an audience as possible. It is aimed both at those who work with software developers and those who aspire to become developers themselves. Unlike most introductions to the command line, which typically assume a relatively high level of technical sophistication, *Learn Enough Command Line to Be Dangerous* assumes no prerequisites other than general computer knowledge (how to launch an application, how to use a web browser, how to [touch type](http://lmgtfy.com/?q=learn+to+touch+type), etc.). Among other things, this means that it doesn’t assume you know [how to use a text editor](http://learnenough.com/text-editor-tutorial), or even what a text editor is. Indeed, this tutorial doesn’t even assume you know what a *command line* is, so if you’re confused by the title, you’re still in the right place. Finally, even if you already know how to use the command line, following this tutorial (and doing the exercises) will help fill in any gaps in your knowledge, and might even teach you a few new things.

> *Note*: To get the most out of this tutorial, join the [Learn Enough Society](http://learnenough.com/story), a subscription service from Learn Enough to Be Dangerous that includes integrated progress tracking, exercise answers, live chat, and streaming videos. See [learnenough.com/story](http://learnenough.com/story) for more information.
>

> Box 1. The magic of computers
>
> Computers may be as close as we get to *magic* in the real world: we type incantations into a machine, and—if the incantations are right—the machine does our bidding. To perform such magic, computer witches and wizards rely not only on words, but also on wands, potions, and an ancient tome or two. Taken together, these tricks of the trade are known as *software development*: computer programming, plus tools like *command lines*, *text editors*, and *version control*. Knowledge of these tools is perhaps the main dividing line between “technical” and “non-technical” people (or, to put it in magical terms, between magicians and [Muggles](https://en.wikipedia.org/wiki/Muggle)). The present tutorial represents the first step needed to cross this technical/non-technical divide. The resulting *technical sophistication* ([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)) will make us software magicians—able to cast computer spells, and get the machine to do our bidding.
>
> My name is [Michael Hartl](http://www.michaelhartl.com/), and I am perhaps best known as the creator of the [Ruby on Rails Tutorial](http://www.railstutorial.org/), a [book](http://railstutorial.org/book) and [screencast series](http://screencasts.railstutorial.org/) that together constitute one of the leading introductions to web development. (You may also know me, in my more mathematical mode, as the founder of [Tau Day](http://tauday.com/) and author of [*The Tau Manifesto*](http://tauday.com/tau-manifesto).) One of the most frequently asked questions about the Rails Tutorial is, “Is the Rails Tutorial good for complete beginners?” The answer is, “Not really.” While it is possible for complete beginners to learn web development with the Ruby on Rails Tutorial (and an impressively large number have), it can be challenging and occasionally frustrating, and I don’t generally recommend it. Instead, I recommend starting here.
>

Many programming tutorials either gloss over the command line or assume you already know how to use it. But understanding the basics of the command line is *absolutely essential* to becoming a skilled developer.[1](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-1) Indeed, if you look at the desktop of an experienced computer programmer, even on a system with a polished graphical user interface like macOS, you are likely to find a large number of “terminal windows”, each containing a series of commands at a command line ([Figure 1](https://www.learnenough.com/command-line-tutorial#fig-dev_desktop)). Proficiency at the command line is also useful for anyone who needs to *work* with developers, such as product managers, project managers, and designers. Making this essential component of technical sophistication accessible to as broad an audience as possible is the goal of *Learn Enough Command Line to Be Dangerous*.

![images/figures/dev_desktop](https://ws4.sinaimg.cn/large/006tNc79gy1fm6ugd17z3j30jg0ay7a0.jpg)

Figure 1: Terminal windows on the desktop of an experienced developer.

## [1Basics](https://www.learnenough.com/command-line-tutorial#sec-basics)

As author [Neal Stephenson](https://en.wikipedia.org/wiki/Neal_Stephenson) famously [put it](http://www.cryptonomicon.com/beginning.html), “In the Beginning was the Command Line.”Although a graphical user interface (GUI) can dramatically simplify computer use, in many contexts the most powerful and flexible way to interact with a computer is through a *command-line interface* (CLI). In such an interface, the [user](http://tron.wikia.com/wiki/User) types *commands* that tell the computer to perform desired tasks. These commands can then be combined in various ways to achieve a variety of outcomes. An example of a typical command-line command appears in [Figure 2](https://www.learnenough.com/command-line-tutorial#fig-command_line_command).

![images/figures/command_line_command](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ugejzxoj30jg0223yq.jpg)

Figure 2: A prototypical command-line command.

This tutorial covers the basics of the Unix command line, where *Unix* refers to a [family of operating systems](https://en.wikipedia.org/wiki/Unix) that includes Linux, Android, iOS (iPhone/iPad), and macOS.[2](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-2) Unix systems serve most of the software on the World Wide Web, run most mobile and tablet devices, and power many of the world’s desktop computers as well. As a result of Unix’s central role in modern computing, this tutorial covers the Unix way of developing software. The main exception to Unix’s dominance is Microsoft® Windows™, which is not part of the Unix tradition, but those who mostly develop using native Windows development tools will still benefit from learning the Unix command line. Among other things, at some point such users are likely to need to issue commands on a Unix server (e.g., via the “secure shell” command `ssh`), at which point familiarity with Unix commands becomes essential. As a result, Windows users are strongly encouraged to run a free *Linux virtual machine* (as described in [Box 2](https://www.learnenough.com/command-line-tutorial#aside-virtual_machine)) in order to get the most out of this tutorial. Another good option is to use a cloud IDE[3](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-3) such as [Cloud9](http://c9.io/); to go this route, follow the “[Development environment](https://www.railstutorial.org/book/beginning#sec-development_environment)” section in the [*Ruby on Rails Tutorial* book](http://railstutorial.org/book).

*Note*: Important commands from this section are summarized in [Table 2](https://www.learnenough.com/command-line-tutorial#table-man_echo).

> Box 2. Running a virtual machine
>
> In order to complete this tutorial, Windows users should install a couple of free programs to run a *virtual machine* (a simulation of a computer) that allows Windows to host a version of the Linux operating system. The steps appear as follows:
>
> 1. Install the right version of [VirtualBox](https://www.virtualbox.org/) for your system (free).
> 2. Download the [Learn Enough Virtual Machine](https://softcover-static.s3.amazonaws.com/LearnEnough-v.1.4.ova) (large file).
> 3. Once the download is complete, double-click the resulting “OVA” file and follow the instructions to install the Virtual Machine (VM).
> 4. Double-click the VM itself and log in using the default user’s password, which is “`foobar!`”.
>
> (Getting all these steps to work is a good exercise in *technical sophistication*, an idea we’ll develop further starting in [Section 1.3](https://www.learnenough.com/command-line-tutorial#sec-man_pages) ([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)).) The result will be a Linux desktop environment (including a command-line terminal program) pre-configured for this tutorial, as shown in [Figure 3](https://www.learnenough.com/command-line-tutorial#fig-virtual_machine).
>
> In the longer run, I recommend switching to a Mac as soon as possible. You might have to save up a bit, as Macs are generally more expensive than Windows machines, but in most cases the increased productivity will quickly pay for the difference. (If you find yourself liking Linux, feel free to stick with it, but Macs are generally easier to use with a better user interface. Plus, you can always run Linux inside a VM, even on a Mac.)
>

![images/figures/virtual_machine](https://ws4.sinaimg.cn/large/006tNc79gy1fm6ughdj6kj30jg0ayjtj.jpg)

Figure 3: A Linux virtual machine running inside a host OS.

### [1.1Running a terminal](https://www.learnenough.com/command-line-tutorial#sec-running_a_terminal)

To run a command-line command, we first need to start a *terminal*, which is the program that gives us a command line. On macOS, you can open a terminal window using the macOS application [*Spotlight*](https://support.apple.com/en-us/HT204014), which you can launch either by typing ⌘␣ (Command-space) or by clicking on the magnifying glass in the upper right part of your screen. Once you’ve launched Spotlight, you can start a terminal program by typing “terminal” in the Spotlight Search bar. (If you are interested in using a more advanced and customizable terminal program, I recommend installing [iTerm](https://www.iterm2.com/), but this step is optional.) On Linux, you can click the terminal icon as shown in [Figure 3](https://www.learnenough.com/command-line-tutorial#fig-virtual_machine).The result should be something like [Figure 4](https://www.learnenough.com/command-line-tutorial#fig-terminal_window), although the exact details on your system will likely differ. If you’re using a different OS, I recommend applying your technical sophistication ([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)) to figure how to open a terminal on your system; for example, to learn how to open a command-line terminal on a [Chromebook](https://www.google.com/chromebook/), you could Google “[how to get a command line on a chromebook](http://lmgtfy.com/?q=how+to+get+a+command+line+on+a+chromebook)”.

![images/figures/terminal_window](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ugih6dzj30jg0d8glv.jpg)

Figure 4: A terminal window.

The example we saw in [Figure 2](https://www.learnenough.com/command-line-tutorial#fig-command_line_command) includes all of the typical elements of a command, as illustrated in [Figure 5](https://www.learnenough.com/command-line-tutorial#fig-anatomy): the *prompt* followed by a *command* (as in “give the computer a command”), an *option* (as in “choose a different option”), and an *argument* (as in the “[argument of a function](https://en.wikipedia.org/wiki/Argument_of_a_function)” in mathematics).[4](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-4) It’s essential to understand that the prompt is supplied automatically by the terminal, and you do not need to type it. (Indeed, if you do type it, it will likely result in an error.) Moreover, the exact details of the prompt will differ, and are not important for the purposes of this tutorial ([Box 3](https://www.learnenough.com/command-line-tutorial#aside-prompt)).

![images/figures/anatomy](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ugleecsj30jg0720u4.jpg)

Figure 5: Anatomy of a command line. (Your prompt may differ.)

> Box 3. What is the prompt?
>
> Every command line starts with some symbol or symbols designed to “prompt” you to action. The prompt usually ends with a dollar sign `$`, and is preceded by information that depends on the details of your system. For example, on some systems the prompt might look like this:
>
> ```
>  Michael's MacBook Air:~ mhartl$
> ```
>
> In [Figure 4](https://www.learnenough.com/command-line-tutorial#fig-terminal_window), the prompt looks like this instead:
>
> ```
>  [~]$
> ```
>
> and in [Figure 5](https://www.learnenough.com/command-line-tutorial#fig-anatomy) it looks like this:
>
> ```
>  [projects]$
> ```
>
> Finally, the prompt I’m looking at right now looks like this:
>
> ```
>  [learn_enough_command_line (master)]$
> ```
>
> For the purposes of this tutorial, the details of the prompt are not important, but we will discuss useful ways to customize the prompt starting in the next tutorial after this one ([*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial)).
>

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_terminal)

*Learn Enough Command Line to Be Dangerous* includes a large number of exercises. I strongly recommend getting in the habit of attempting them before moving on to the next section, as they reinforce the material we’ve just covered and will give you essential practice in using the many commands discussed. It’s not generally the case that they are *required* to proceed, though, so if you get stuck it’s sometimes a good idea to continue forward and then revisit the exercise at a later time. Indeed, this is good advice for the main text as well—you’ll be surprised how often a seemingly impossible idea or intractable problem will look easy the second time around.

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. By referring to [Figure 5](https://www.learnenough.com/command-line-tutorial#fig-anatomy), identify the prompt, command, options, arguments, and cursor in each line of [Figure 6](https://www.learnenough.com/command-line-tutorial#fig-command_exercise).
2. Most modern terminal programs have the ability to create multiple *tabs* ([Figure 7](https://www.learnenough.com/command-line-tutorial#fig-terminal_tabs)), which are useful for organizing a set of related terminal windows.[5](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-5) By examining the menu items for your terminal program ([Figure 8](https://www.learnenough.com/command-line-tutorial#fig-terminal_menu)), figure out how to create a new tab. *Extra credit*: Learn the keyboard shortcut for creating a new tab. (Learning keyboard shortcuts for your system is an excellent habit to cultivate.)

![images/figures/command_exercise](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ugo5dc0j30jg0fsgod.jpg)

Figure 6: A series of typical commands.

![images/figures/terminal_tabs](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ugsrjq6j30jg0fq0y8.jpg)

Figure 7: A terminal window with three tabs.

![images/figures/terminal_menu](https://ws4.sinaimg.cn/large/006tNc79gy1fm6ugxd7s4j30hg0g8mza.jpg)

Figure 8: Some menu items for the default macOS terminal.

### [1.2Our first command](https://www.learnenough.com/command-line-tutorial#sec-our_first_command)

We are now prepared to run our first command, which prints the word “hello” to the screen. (The place where characters get printed is known as “standard out”, which is usually just the screen, and rarely refers to a physical printer.) The command is `echo`, and the argument is the string of characters—or simply *string* for short—that we want to print. To run the `echo` command, type “echo hello” at the prompt, and then press the Return key (also called Enter):

```
$ echo hello
hello
$

```

(I recommend always typing the commands out yourself, which will let you learn more than if you rely on copying and pasting.) Here we see that `echo hello` prints “hello” and then returns another prompt. Note that, for brevity, I’ve omitted all characters in the prompt except the dollar sign `$`.

Just to make the pattern clear, let’s try a second `echo` command:

```
$ echo "goodbye"
goodbye
$ echo 'goodbye'
goodbye
$

```

Note here that we’ve wrapped “goodbye” in quotation marks—and we also see that we can use either double quotes, as in `"goodbye"`, or single quotes, as in `’goodbye’`. Such quotes can be used to group strings visually, though in many contexts they are not required by `echo`([Listing 1](https://www.learnenough.com/command-line-tutorial#code-hello_goodbye)).[6](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-6)

Listing 1: Printing “hello, goodbye” two different ways.

```
$ echo hello, goodbye
hello, goodbye
$ echo "hello, goodbye"
hello, goodbye
$

```

One thing that can happen when using quotes is accidentally not matching them, as follows:

```
$ echo "hello, goodbye
>

```

At this point, it seems we’re stuck. There are specific ways out of this quandary (in fact, in this case you can just add a closing quote and hit return), but it’s good to have a general strategy for getting out of trouble ([Figure 9](https://www.learnenough.com/command-line-tutorial#fig-cat_in_box)).[7](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-7) This strategy is called “Ctrl-C” ([Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble)).

![images/figures/cat_in_box](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uh2946tj30jg0asjwz.jpg)

Figure 9: This cat appears to be stuck and should probably hit `Ctrl-C`.

> Box 4. Getting out of trouble
>
> When using the command line, there are lots of things that can get you in trouble, by which I mean the terminal will just hang or otherwise end up in a state that makes entering further commands difficult or impossible. Here are some examples of such commands:
>
> ```
>  $ echo "hello
> ```
>
> ```
>  $ grep foobar
> ```
>
> ```
>  $ yes
> ```
>
> ```
>  $ tail
> ```
>
> ```
>  $ cat
> ```
>
> In every case, the solution is the same: hit `Ctrl-C` (pronounced “control-see”). Here `Ctrl` refers to the “control” key on your keyboard, and `C` refers to the key labeled “C”. `Ctrl-C` thus means “While holding down the control key, press C.” In particular, `C`does *not* refer to the capital letter C, so you should not press Shift in addition to Ctrl.(`Ctrl-C` sends a *control code* to the terminal and has nothing to do with producing a capital C when typing normal text.) The result of typing `Ctrl-C` is sometimes written as `⌃C`, like this:
>
> ```
>  $ tail
>  ^C
> ```
>
> The [origins of `Ctrl-C`](https://en.wikipedia.org/wiki/Control-C) are somewhat obscure, but as a mnemonic I like to think of it as meaning “cancel”. However you remember it, *do* remember it: when you get into trouble at the command line, your best bet is usually to hit `Ctrl-C`.
>
> *Note*: When `Ctrl-C` fails, 90% of the time hitting `ESC` (escape) will do the trick.
>

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_first_command)

> Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).
>

1. Write a command that prints out the string “hello, world”. *Extra credit*: As in [Listing 1](https://www.learnenough.com/command-line-tutorial#code-hello_goodbye), do it two different ways, both with and without using quotation marks.
2. Type the command `echo ’hello` (with a mismatched single quote), and then get out of trouble using the technique from [Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble).

### [1.3Man pages](https://www.learnenough.com/command-line-tutorial#sec-man_pages)

The program we’re using to run a command line, which is technically known as a *shell*,[8](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-8) includes a powerful (though often cryptic) tool to learn more about available commands. This tool is itself a command-line command called `man` (short for “manual”). Its argument is the name of the command (such as `echo`) that we want to learn more about. The details are system-dependent, but on my system the result of running `man echo` appears as in [Listing 2](https://www.learnenough.com/command-line-tutorial#code-man_echo).

Listing 2: The result of running `man echo`.

```
$ man echo
ECHO(1)          BSD General Commands Manual         ECHO(1)

NAME
   echo -- write arguments to the standard output

SYNOPSIS
   echo [-n] [string ...]

DESCRIPTION
   The echo utility writes any specified operands, separated by single blank
   (` ') characters and followed by a newline (`\n') character, to the stan-
   dard output.

   The following option is available:

   -n  Do not print the trailing newline character. This may also be
      achieved by appending `\c' to the end of the string, as is done by
      iBCS2 compatible systems. Note that this option as well as the
      effect of `\c' are implementation-defined in IEEE Std 1003.1-2001
      (``POSIX.1'') as amended by Cor. 1-2002. Applications aiming for
      maximum portability are strongly encouraged to use printf(1) to
      suppress the newline character.
:                                                                             

```

On the last line of [Listing 2](https://www.learnenough.com/command-line-tutorial#code-man_echo), note the presence of a colon `:`, which indicates that there is more information below. The details of this last line are system-dependent, but on any system you should be able to access subsequent information one line at a time by pressing the down arrow key, or one page at a time by pressing the spacebar. To exit the man page, press “q” (for “quit”).(This interface to the man pages is the same as for the `less` program, which we’ll learn about in [Section 3.3](https://www.learnenough.com/command-line-tutorial#sec-less_is_more).)

![images/figures/man_to_man](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uh6wbbqj30jg0czaeu.jpg)

Figure 10: Applying `man` to `man`.

Because `man` itself is a command, we can apply `man` to `man` ([Figure 10](https://www.learnenough.com/command-line-tutorial#fig-man_to_man)),[9](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-9) as shown in [Listing 3](https://www.learnenough.com/command-line-tutorial#code-man_man).

Listing 3: The result of running `man man`.

```
$ man man
man(1)                                 man(1)

NAME
    man - format and display the on-line manual pages

SYNOPSIS
    man [-acdfFhkKtwW] [--path] [-m system] [-p string] [-C config_file]
    [-M pathlist] [-P pager] [-B browser] [-H htmlpager] [-S section_list]
    [section] name ...

DESCRIPTION
    man formats and displays the on-line manual pages. If you specify sec-
    tion, man only looks in that section of the manual. name is normally
    the name of the manual page, which is typically the name of a command,
    function, or file. However, if name contains a slash (/) then man
    interprets it as a file specification, so that you can do man ./foo.5
    or even man /cd/foo/bar.1.gz.

    See below for a description of where man looks for the manual page
    files.

OPTIONS
    -C config_file
:

```

We can see from [Listing 3](https://www.learnenough.com/command-line-tutorial#code-man_man) that the synopsis of `man` looks something like this:

```
man [-acdfFhkKtwW] [--path] [-m system] [-p string] ...

```

This is what I meant above when I described man pages as “often cryptic”. Indeed, in many cases I find the details of man pages to be almost impossible to understand, but being able to scan over the man page to get a high-level overview of a command is a valuable skill, one worth acquiring.To get used to reading man pages, I recommend running `man <command name>` when encountering a new command. Even if the details aren’t entirely clear, reading the man pages will help develop the valuable skill of *technical sophistication* ([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)).[10](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-10)

> Box 5. Technical sophistication
>
> In mathematics, many subjects can be developed by applying pure deduction to a small number of assumptions, or *axioms*; examples include algebra, geometry, number theory, and analysis. As a result, such subjects are completely self-contained, and thus have no formal prerequisites—in principle, even a small child could learn them. In practice, though, something else is required, and mathematicians often recommend the informal prerequisite of *mathematical maturity*, which consists of the experience and general sophistication needed to understand and write mathematical proofs.
>
> In technology, a similar skill (or, more accurately, set of skills) exists in the form of *technical sophistication*. In addition to “hard skills” like familiarity with text editors and the Unix command line, technical sophistication includes “soft skills” like looking for promising menu items and knowing the kinds of search terms to drop into Google ([Figure 11](https://www.learnenough.com/command-line-tutorial#fig-tech_support_cheat_sheet)), along with an *attitude* of doing what it takes to make the machine do our bidding ([Box 1](https://www.learnenough.com/command-line-tutorial#aside-computer_magic)). These soft skills, and this attitude, are hard to teach directly, so as you progress through this and subsequent [Learn Enough tutorials](http://learnenough.com/) you should always be on the lookout for opportunities to increase your technical sophistication (such as, for example, learning how to get the gist of a program by scanning its man page ([Section 1.3](https://www.learnenough.com/command-line-tutorial#sec-man_pages))). Over time, the cumulative effect will be that, like the author of [Figure 11](https://www.learnenough.com/command-line-tutorial#fig-tech_support_cheat_sheet), you’ll have the seemingly magical ability to do everything in every program.
>
> By the way, [Figure 11](https://www.learnenough.com/command-line-tutorial#fig-tech_support_cheat_sheet) is missing three important techniques for solving common problems:
>
> 1. Have you restarted the application?
>
> 2. Have you rebooted the device?
>
> 3. Have you tried uninstalling and reinstalling the app?
>
>    #2 alone probably solves 90% of unexplained computer errors.
>

![images/figures/tech_support_cheat_sheet](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uhb4pa3j30kc0mvq4w.jpg)

Figure 11: “[Tech Support Cheat Sheet](https://m.xkcd.com/627/)” (via [xkcd](http://xkcd.com/)). See [Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication) for three extra techniques.

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_man)

> Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).
>

1. According to the man page, what are the official short and long descriptions of `echo` on your system?

2. As seen in



   Listing 1

   , by default the



   ```
   echo
   ```



   command prints its argument to the screen and then puts the new prompt on a new line.

   ​



   The way it does this is by appending a special character called a



   *newline*



   (a special character that literally puts the string on a new line, written in many contexts as “backslash n”

   ```
   \n
   ```

   ).

   ​



   Because



   ```
   echo
   ```



   is often used in programs to print out a sequence of strings



   not



   separated by newlines, there is a special command-line option to prevent the newline from being inserted.

   By reading the man page for `echo`, determine the command needed to print out “hello” *without* the trailing newline, and verify using your terminal that it works as expected.*Hints*: To determine the placement of the command-line option, it may help to refer to [Figure 5](https://www.learnenough.com/command-line-tutorial#fig-anatomy). By comparing your result with [Listing 4](https://www.learnenough.com/command-line-tutorial#code-with_newline) and [Listing 5](https://www.learnenough.com/command-line-tutorial#code-without_newline), you should be able to verify that you’ve used the option properly. (*Note*: This exercise may fail when using the default terminal program on some older versions of macOS. In this case, I recommend installing [iTerm](https://www.iterm2.com/) (which isn’t a bad idea anyway).)

Listing 4: The result of running `echo` with a newline (without option).

```
hello
[~]$

```

Listing 5: The result of running `echo` without a newline (*with* option).

```
hello[~]$

```

### [1.4Editing the line](https://www.learnenough.com/command-line-tutorial#sec-editing_the_line)

Command lines include several features to make it easy to repeat previous commands, possibly in edited form. These and many other command-line features often involve special keys on the keyboard, so for reference [Table 1](https://www.learnenough.com/command-line-tutorial#table-keyboard_symbols) shows these symbols for the various keys on a typical Macintosh keyboard. Apply your technical sophistication ([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)) if your keyboard differs.

| **Key**               | **Symbol** |
| --------------------- | ---------- |
| Command               | ⌘          |
| Control               | ⌃          |
| Shift                 | ⇧          |
| Option                | ⌥          |
| Up, down, left, right | ↑ ↓ ← →    |
| Enter/Return          | ↵          |
| Tab                   | ⇥          |
| Delete                | ⌫          |

Table 1: Miscellaneous keyboard symbols.

One of the most useful ways to edit the line is to “up arrow” ↑, which simply retrieves the previous command. Pressing up arrow again moves further up the list of commands, while “down arrow” ↓ goes back toward the bottom.

Other common ways to edit the line use the control key, which (as we saw in [Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble)) is usually written as `Ctrl` or `⌃`. For example, when typing a new command, or dealing with a previous command, it is often convenient to be able to move quickly within the line. Suppose we typed

```
$ goodbye

```

only to realize that we wanted to put `echo` in front of it. We could use the left arrow key ← to get to the beginning of the line, but it’s easier to type `⌃A`, which takes us there immediately.Similarly, `⌃E` moves to the end of the line.[11](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-11) Finally, `⌃U` clears to the beginning of the line and lets us start over.

The combination of `⌃A`, `⌃E`, and `⌃U` will work on most systems, but they don’t do you much good if you’re editing a longer line, such as this one containing the first line of [Sonnet 1 by William Shakespeare](http://www.shakespeares-sonnets.com/sonnet/1) ([Listing 6](https://www.learnenough.com/command-line-tutorial#code-sonnet_1)).

Listing 6: Printing the first line of Shakespeare’s first sonnet.

```
$ echo "From fairest creatures we desire increase,"

```

Suppose we wanted to change “From” to “FRom” to more closely match the text from the original sonnet ([Figure 12](https://www.learnenough.com/command-line-tutorial#fig-sonnet_1)).[12](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-12) We could type `⌃A` followed by the right arrow key a few times, but on some systems it’s possible to move directly to the desired spot by combining the keyboard and mouse via Option-click. That is, you can hold down the Option key on your keyboard (if it exists),[13](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-13) and then click with the mouse pointer on the place in the command where you want the cursor. This would let us move right to the “o” in “From”, allowing us to delete the “r” and yielding [Listing 7](https://www.learnenough.com/command-line-tutorial#code-sonnet_1_edited) directly.

![images/figures/Sonnet_1](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uhmj8ygj30au085js9.jpg)

Figure 12: The original appearance of Shakespeare’s first sonnet.

Listing 7: The result of editing a longer command-line command.

```
$ echo "FRom fairest creatures we desire increase,"

```

I usually move around the command line with a combination of `⌃A`, `⌃E`, and right & left arrow keys, but for longer commands Option-click can be a big help. (I also frequently change my mind about the exact command I’m typing, in which case I usually find that hitting `⌃U` and starting over again is the fastest way to proceed.)

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_editing_the_line)

> Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).
>

1. Using the up arrow, print to the screen the strings “fee”, “fie”, “foe”, and “fum” without retyping `echo` each time.
2. Starting with the line in [Listing 6](https://www.learnenough.com/command-line-tutorial#code-sonnet_1), use any combination of `⌃A`, `⌃E`, arrow keys, or Option-click to change the occurrences of the short s to the archaic [long s](https://en.wikipedia.org/wiki/Long_s) “ſ” in order to match the appearance of the original ([Figure 12](https://www.learnenough.com/command-line-tutorial#fig-sonnet_1)). In other words, the argument to `echo`should read “FRom faireſt creatures we deſire increaſe,”. *Hint*: It’s unlikely that your keyboard can produce “ſ” natively, so either copy it from the text of this tutorial or [Google for it](http://lmgtfy.com/?q=unicode+long+s) and copy it from the Internet. (If you have trouble copying and pasting into your terminal, I suggest applying the ideas in [Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication) to figure out how to do it on your system.)

### [1.5Cleaning up](https://www.learnenough.com/command-line-tutorial#sec-cleaning_up)

When using the command line, sometimes it’s convenient to be able to clean up by clearing the screen, which we can do with `clear`:

```
$ clear

```

A keyboard shortcut for this is `⌃L`.

Similarly, when we are done with a terminal window (or tab) and are ready to exit, we can use the `exit` command:

```
$ exit

```

A keyboard shortcut for this is `⌃D`.

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_cleaning)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Clear the contents of the current tab.
2. Open a new tab, execute `echo ’hello’`, and then exit.

### [1.6Summary](https://www.learnenough.com/command-line-tutorial#sec-summary_cleaning)

Important commands from this section are summarized in [Table 2](https://www.learnenough.com/command-line-tutorial#table-man_echo).

| **Command**     | **Description**                  | **Example**    |
| --------------- | -------------------------------- | -------------- |
| `echo <string>` | Print string to screen           | `$ echo hello` |
| `man <command>` | Display manual page for command  | `$ man echo`   |
| `⌃C`            | Get out of trouble               | `$ tail``^C`   |
| `⌃A`            | Move to beginning of line        |                |
| `⌃E`            | Move to end of line              |                |
| `⌃U`            | Delete to beginning of line      |                |
| Option-click    | Move cursor to location clicked  |                |
| Up & down arrow | Scroll through previous commands |                |
| `clear` or `⌃L` | Clear screen                     | `$ clear`      |
| `exit` or `⌃D`  | Exit terminal                    | `$ exit`       |

Table 2: Important commands from [Section 1](https://www.learnenough.com/command-line-tutorial#sec-basics).

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_summary_basics)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Write a command to print the string `Use "man echo"`, *including* the quotes; i.e., take care not to print out `Use man echo` instead. *Hint*: Use double quotes in the inner string, and wrap the whole thing in single quotes.
2. By running `man sleep`, figure out how to make the terminal “sleep” for 5 seconds, and execute the command to do so.
3. Execute the command to sleep for 5000 seconds, realize that’s well over an hour, and then use the instructions from [Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble) to get out of trouble.

## [2Manipulating files](https://www.learnenough.com/command-line-tutorial#sec-manipulating_files)

Having covered how to run a basic command, we’re now ready to learn how to manipulate files, one of the most important tasks at the command line. Because this tutorial assumes no technical prerequisites, we’re not going to require any familiarity with programs designed to edit text.(Such programs, called *text editors*, are the subject of the next tutorial in the sequence, [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial).) This means that we’ll need to create files by hand at the command line. But this is a feature, not a bug ([Box 6](https://www.learnenough.com/command-line-tutorial#aside-speak_geek)), because learning to create files at the command line is a valuable skill in itself.

*Note*: Important commands from this section are summarized in [Table 3](https://www.learnenough.com/command-line-tutorial#table-manipulating_files).

> Box 6. Learning to speak “geek”
>
> One important part of learning software development is becoming familiar with the [hacker](http://www.catb.org/~esr/faqs/hacker-howto.html), nerd, and geek culture from which much of it springs. For example, the phrase “It’s not a bug, it’s a feature” is a common way of recasting a seeming flaw as a virtue. As the Urban Dictionary [puts it](http://www.urbandictionary.com/define.php?term=It%27s+not+a+bug%2C+it%27s+a+feature&defid=6751775):
>
> > **It’s not a bug, it’s a feature**
> >
> > Excuse made by software developers when they try to convince the user that a flaw in their program is actually what it’s supposed to be doing.
>
> The [Jargon File](http://www.catb.org/jargon/html/), which includes an [enormous and entertaining lexicon](http://www.catb.org/jargon/html/go01.html) of hacker terms, expands on this theme in its entry on [*feature*](http://www.catb.org/jargon/html/F/feature.html):
>
> > “Undocumented feature” is a common, allegedly humorous euphemism for a [*bug*](http://www.catb.org/jargon/html/B/bug.html).There’s a related joke that is sometimes referred to as the “one-question geek test”.You say to someone “I saw a Volkswagen Beetle today with a vanity license plate that read FEATURE”. If he/she laughs, he/she is a [*geek*](http://www.catb.org/jargon/html/G/geek.html).
>
> The joke here is that, because “bug” is a common slang term for a Volkswagen Beetle, a Beetle with the vanity plate FEATURE is a real-life manifestation of “It’s not a bug, it’s a feature” ([Figure 13](https://www.learnenough.com/command-line-tutorial#fig-bug_feature)).
>
> Even if you’re not a geek or nerd yourself, learning to “speak geek” will help you navigate both the technological landscape and the social world that surrounds it.
>

![images/figures/bug_feature](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uhrm88hj30dw0900x9.jpg)

Figure 13: It’s not a bug, it’s a feature.

### [2.1Redirecting and appending](https://www.learnenough.com/command-line-tutorial#sec-redirecting_and_appending)

Let’s pick up (more or less) where we left off in [Section 1](https://www.learnenough.com/command-line-tutorial#sec-basics), with an `echo` command to print out the first line of Shakespeare’s first sonnet ([Listing 6](https://www.learnenough.com/command-line-tutorial#code-sonnet_1)):

```
$ echo "From fairest creatures we desire increase,"
From fairest creatures we desire increase,

```

Our task now is to create a file containing this line. Even without the benefit of a text editor, it is possible to do this using the *redirect operator* `>`:

```
$ echo "From fairest creatures we desire increase," > sonnet_1.txt

```

(Recall that you can use up arrow to retrieve the previous command rather than typing it from scratch.) Here the right angle bracket `>` takes the string output from `echo` and redirects its contents to a file called `sonnet_1.txt`.

How can we tell if the redirect worked? We’ll learn some more advanced command-line tools for inspecting files in [Section 3](https://www.learnenough.com/command-line-tutorial#sec-inspecting_files), but for now we’ll use the `cat` command, which simply dumps the contents of the file to the screen:

```
$ cat sonnet_1.txt
From fairest creatures we desire increase,

```

The name `cat` is short for “[concatenate](http://dictionary.reference.com/browse/concatenate)”, which is a hint that it can be used to combine the contents of multiple files, but the usage above (to dump the contents of a single file to the screen) is extremely common. Think of `cat` as a “quick-and-dirty” way to view the contents of a particular file ([Figure 14](https://www.learnenough.com/command-line-tutorial#fig-cat)).[14](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-14)

![cat](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uhutzdtj30gu0ayai2.jpg)

Figure 14: Viewing a file with `cat`.

In order to add the second line of the sonnet (in modernized spelling), we can use the *append operator* `>>` as follows:

```
$ echo "That thereby beauty's Rose might never die," >> sonnet_1.txt

```

This just adds the line to the end of the given file. As before, we can see the result using `cat`:

```
$ cat sonnet_1.txt
From fairest creatures we desire increase,
That thereby beauty's Rose might never die,

```

(To get to this command, I hope you just hit up arrow twice instead of retyping it. If so, you’re definitely getting the hang of this.) The result above shows that the double right angle bracket `>>` appended the string from `echo` to the file `sonnet_1.txt` as expected.

Modernized treatments of the *Sonnets* sometimes [emend](http://dictionary.reference.com/browse/emend) *Rose* to *rose* (thereby obscuring the [likely meaning](https://en.wikipedia.org/wiki/Tudor_rose)), and we can make a second file following this convention using two more calls to `echo`:

```
$ echo "From fairest creatures we desire increase," > sonnet_1_lower_case.txt
$ echo "That thereby beauty's rose might never die," >> sonnet_1_lower_case.txt

```

In order to facilitate the comparison of files that are similar but not identical, Unix systems come with the helpful `diff` command:

```
$ diff sonnet_1.txt sonnet_1_lower_case.txt
< That thereby beauty's Rose might never die,
---
> That thereby beauty's rose might never die,

```

When discussing computer files, *diff* is frequently employed both as a noun (“What’s the diff between those files?”) and as a verb (“You should diff the files to see what changed.”). As with many technical terms, this sometimes bleeds over into common usage, such as “Diff present ideas against those of various past cultures, and see what you get.”[15](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-15)

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_redirecting_appending)

At the end of each of the exercises below, use the `cat` command to verify your answer.

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Using `echo` and `>`, make files called `line_1.txt` and `line_2.txt` containing the first and second lines of Sonnet 1, respectively.
2. Replicate the original `sonnet_1.txt` (containing the first two lines of the sonnet) by first redirecting the contents of `line_1.txt` and then appending the contents of `line_2.txt`. Call the new file `sonnet_1_copy.txt`, and confirm using `diff` that it’s identical to `sonnet_1.txt`. *Hint*: When there is no diff between two files, `diff` simply outputs nothing.
3. Use `cat` to combine the contents of `line_1.txt` and `line_2.txt` in reverse order using a *single* command, yielding the file `sonnet_1_reversed.txt`. *Hint*: The `cat`command can take multiple arguments.

### [2.2Listing](https://www.learnenough.com/command-line-tutorial#sec-listing)

Perhaps the mostly frequently typed command on the Unix command line is `ls`, short for “list” ([Listing 8](https://www.learnenough.com/command-line-tutorial#code-ls)).

Listing 8: Listing files and directories with `ls`. (Output will vary.)

```
$ ls
Desktop
Downloads
sonnet_1.txt
sonnet_1_reversed.txt

```

The `ls` command simply lists all the files and directories in the current directory (except for those that are *hidden*, which we’ll learn more about in a moment). In this sense, it’s effectively a command-line version of the graphical browser used to show files and directories (also called “folders”), as seen in [Figure 15](https://www.learnenough.com/command-line-tutorial#fig-file_listing). (We’ll sharpen our understanding of directories and folders in [Section 4](https://www.learnenough.com/command-line-tutorial#sec-directories).) As with a graphical file browser, the output in [Listing 8](https://www.learnenough.com/command-line-tutorial#code-ls) is just a sample, and results will differ based on the details of your system. (This goes for all the `ls` examples, so don’t be concerned if there are minor differences in output.)

![images/figures/file_listing](https://ws2.sinaimg.cn/large/006tNc79gy1fm6ui34mfpj30jg09kgod.jpg)

Figure 15: The graphical equivalent of `ls`.

The `ls` command can be used to check if a file (or directory) exists, because trying to `ls` a nonexistent file results in an error message, as seen in [Listing 9](https://www.learnenough.com/command-line-tutorial#code-ls_no_such).

Listing 9: Running `ls` on a nonexistent file.

```
$ ls foo
ls: foo: No such file or directory
$ touch foo
$ ls foo
foo

```

[Listing 9](https://www.learnenough.com/command-line-tutorial#code-ls_no_such) uses the `touch` command to create an empty file with the name `foo` ([Box 7](https://www.learnenough.com/command-line-tutorial#aside-foo_bar)), so the second time we run `ls` the error message is gone. (The stated purpose of `touch` is to change the modification time on files or directories, but (ab)using `touch` to create empty files as in [Listing 9](https://www.learnenough.com/command-line-tutorial#code-ls_no_such) is a common Unix idiom.)

> Box 7. Foo, bar, baz, etc.
>
> When reading about computers, you will encounter certain strange words—words like *foo*, *bar*, and *baz*—with surprising frequency. Indeed, in addition to `ls foo` and `touch foo`, we have already seen four such references in this tutorial: in a typical command-line command ([Figure 2](https://www.learnenough.com/command-line-tutorial#fig-command_line_command)), in a virtual machine password (`foobar!`, [Box 2](https://www.learnenough.com/command-line-tutorial#aside-virtual_machine)), again when getting out of trouble (`grep foobar`, [Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble)), and yet again in a man page ([Listing 3](https://www.learnenough.com/command-line-tutorial#code-man_man)).The first three were my own uses, but the last I had nothing to do with:
>
> ```
>  ...if name contains a slash (/) then man interprets
>  it as a file specification,  so that you can do man
>  ./foo.5 or even man /cd/foo/bar.1.gz.
> ```
>
> Here we see both *foo* and *bar* making an appearance in the man page for `man` itself—an unambiguous testament to their ubiquity in computing.
>
> What is the origin of these odd terms? As usual, the [Jargon File](http://www.catb.org/jargon/html/) (via its entry on [*foo*](http://www.catb.org/jargon/html/F/foo.html)) enlightens us:
>
> > **foo**: /foo/
> >
> > 1. interj. Term of disgust.
> >
> > 2. [very common] Used very generally as a sample name for absolutely anything, esp. programs and files (esp. scratch files).
> >
> > 3. First on the standard list of [metasyntactic variable](http://www.catb.org/jargon/html/M/metasyntactic-variable.html)s used in syntax examples. See also [bar](http://www.catb.org/jargon/html/B/bar.html), [baz](http://www.catb.org/jargon/html/B/baz.html), [qux](http://www.catb.org/jargon/html/Q/qux.html), [quux](http://www.catb.org/jargon/html/Q/quux.html), etc.
> >
> > When ‘foo’ is used in connection with ‘bar’ it has generally traced to the WWII-era Army slang acronym [*FUBAR*](http://www.catb.org/jargon/html/F/FUBAR.html) [[see original meaning](http://www.urbandictionary.com/define.php?term=fubar)], later modified to [*foobar*](http://www.catb.org/jargon/html/F/foobar.html).Early versions of the Jargon File interpreted this change as a post-war bowdlerization, but it now seems more likely that FUBAR was itself a derivative of ‘foo’ perhaps influenced by German *furchtbar* (terrible) — ‘foobar’ may actually have been the *original* form.
>
> Following the link to [metasyntactic variable](http://www.catb.org/jargon/html/M/metasyntactic-variable.html)s, we then find the following:
>
> > **metasyntactic variable**: n.
> >
> > A name used in examples and understood to stand for whatever thing is under discussion, or any random member of a class of things under discussion. The word foo is the canonical example. To avoid confusion, hackers never (well, hardly ever) use ‘foo’ or other words like it as permanent names for anything. In filenames, a common convention is that any filename beginning with a metasyntactic-variable name is a scratch file that may be deleted at any time.
> >
> > Metasyntactic variables are so called because (1) they are variables in the metalanguage used to talk about programs, etc.; (2) they are variables whose values are often variables (as in usages like “the value of f(foo,bar) is the sum of foo and bar”). However, it has been plausibly suggested that the real reason for the term “metasyntactic variable” is that it sounds good.
>
> In other words, if you want to create a file, and the name doesn’t matter, the name is usually “foo”. Once you’ve used “foo”, the next file is called “bar”, the one after that “baz”.Continuations from there vary (“quux” is one [common choice](http://www.catb.org/jargon/html/Q/quux.html)), but in many cases three is enough.
>

A common pattern when using the command line is changing directories using `cd` (covered in [Section 4](https://www.learnenough.com/command-line-tutorial#sec-directories)) and then immediately typing `ls` to view the contents of the directory. This lets us orient ourselves, and is a good first step toward whatever our next action might be.

One useful ability of `ls` is support for the *wildcard character* `*` (read “star”). For example, to list all files ending in “.txt”, we would type this:

```
$ ls *.txt
sonnet_1.txt
sonnet_1_reversed.txt

```

Here `*.txt` (read “star dot tee-ex-tee”) automatically expands to all the filenames that match the pattern “any string followed by .txt”.

There are three particularly important optional forms of `ls`, starting with the “long form”, using the option `-l` (read “dash-ell”):

```
$ ls -l *.txt
total 16
-rw-r--r-- 1 mhartl staff  87 Jul 20 18:05 sonnet_1.txt
-rw-r--r-- 1 mhartl staff 294 Jul 21 12:09 sonnet_1_reversed.txt

```

For now, you can safely ignore most of the information output by `ls -l`, but note that the long form lists a date and time indicating the last time the file was modified. The number before the date is the *size* of the file, in bytes.[16](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-16)

A second powerful `ls` variant is “list by **r**eversed **t**ime of modification (**l**ong format)”, or `ls -rtl`, which lists the long form of each file or directory in order of how recently it was modified (*reversed* so that the most recently modified entries appear at the bottom of the screen for easy inspection). This is particularly useful when there are a lot of files in the directory but you really only care about seeing the ones that have been modified recently, such when confirming a file download. We’ll see an example of this in [Section 3.1](https://www.learnenough.com/command-line-tutorial#sec-downloading_a_file), but you are free to try it now:

```
$ ls -rtl
<results system-dependent>

```

By the way, `-rtl` is the commonly used compact form, but you can also pass the options individually, like this:

```
$ ls -r -t -l

```

In addition, their order is irrelevant, so typing `ls -trl` gives the same result.

#### [Hidden files](https://www.learnenough.com/command-line-tutorial#sec-hidden_files)

Finally, Unix has the concept of “hidden files (and directories)”, which don’t show up by default when listing files. Hidden files and directories are identified by starting with a dot `.`, and are commonly used for things like storing user preferences. For example, in [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git), we’ll create a file called `.gitignore` that tells a particular program (Git) to ignore files matching certain patterns. As a concrete example, to ignore all files ending in “.txt”, we could do this:

```
$ echo "*.txt" > .gitignore
$ cat .gitignore
*.txt

```

If we then run `ls`, the file won’t show up, because it’s hidden:

```
$ ls
sonnet_1.txt
sonnet_1_reversed.txt

```

To get `ls` to display hidden files and directories, we need to pass it the `-a` option (for “all”):

```
$ ls -a
.           .gitignore      sonnet_1_reversed.txt
..          sonnet_1.txt

```

Now `.gitignore` shows up, as expected. (We’ll learn what `.` and `..` refer to in [Section 4.3](https://www.learnenough.com/command-line-tutorial#sec-navigating_directories).)

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_listing)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. What’s the command to list all the non-hidden files and directories that start with the letter “s”?
2. What is the command to list all the non-hidden files that contain the string “onnet”, long-form by reverse modification time? *Hint*: Use the wildcard operator at both the beginning and the end.
3. What is the command to list *all* files (including hidden ones) by reverse modification time, in long form?

### [2.3Renaming, copying, deleting](https://www.learnenough.com/command-line-tutorial#sec-renaming_copying_deleting)

Next to listing files, probably the most common file operations involve renaming, copying, and deleting them. As with listing files, most modern operating systems provide a graphical user interface to such tasks, but in many contexts it is more convenient to perform them at the command line.

The way to rename a file is with the `mv` command, short for “move”:

```
$ echo "test text" > test
$ mv test test_file.txt
$ ls
test_file.txt

```

This renames the file called `test` to `test_file.txt`. The final step in the example runs `ls`to confirm that the file renaming was successful, but system-specific files other than the test file are omitted from the output shown. (The name “move” comes from the general use of `mv` to move a file to a different directory ([Section 4](https://www.learnenough.com/command-line-tutorial#sec-directories)), possibly renaming it en route. When the origin and target directories coincide, such a “move” reduces to a simple renaming.)

The way to copy a file is with `cp`, short for “copy”:

```
$ cp test_file.txt second_test.txt
$ ls
second_test.txt
test_file.txt

```

Finally, the command for deleting a file is `rm`, for “remove”:

```
$ rm second_test.txt
remove second_test.txt? y
$ ls second_test.txt
ls: second_test.txt: No such file or directory

```

Note that, on many systems, by default you will be prompted to confirm the removal of the file.Any answer starting with the letter “y” or “Y” will cause the file to be deleted, and any other answers will prevent the deletion from occurring.

By the way, in the calls to `cp` and `rm` above, I would almost certainly not type out `test_file.txt` or `second_test.txt`. Instead, I would type something like `test⇥` or `sec⇥` (where ⇥ represents the tab key ([Table 1](https://www.learnenough.com/command-line-tutorial#table-keyboard_symbols))), thereby making use of *tab completion*([Box 8](https://www.learnenough.com/command-line-tutorial#aside-tab_completion)).

> Box 8. Tab completion
>
> Most modern command-line programs (shells) support *tab completion*, which involves automatically completing a word if there’s only one valid match on the system. For example, if the only file starting with the letters “tes” is `test_file`, we could create the command to remove it as follows:
>
> ```
>  $ rm tes⇥
> ```
>
> where ⇥ is the tab key ([Table 1](https://www.learnenough.com/command-line-tutorial#table-keyboard_symbols)). The shell would then complete the filename, yielding `rm test_file`. Especially with longer filenames (or directories), tab completion can save a huge amount of typing. It also lowers the [*cognitive load*](https://en.wikipedia.org/wiki/Cognitive_load), since it means you don’t have to remember the full name of the file—only its first few letters.
>
> If the match is ambiguous, as would happen if we had files called `foobarquux` and `foobazquux`, the word will be completed only as far as possible, so
>
> ```
>  $ ls foo⇥
> ```
>
> would be completed to
>
> ```
>  $ ls fooba
> ```
>
> If we then hit tab *again*, we would see a list of matches:
>
> ```
>  $ ls fooba⇥
>  foobarquux foobazquux
> ```
>
> We could then type more letters to resolve the ambiguity, so typing the `r` after `fooba`and hitting `⇥` would yield
>
> ```
>  $ ls foobar⇥
> ```
>
> which would be completed to `foobarquux`. This situation is common enough that experienced command-line users will often just hit something like `f⇥⇥` to get the shell to show all the possibilities:
>
> ```
>  $ ls f⇥⇥
>  figure_1.png foobarquux  foobazquux
> ```
>
> Additional letters would then be typed as usual to resolve the ambiguity.
>

The default behavior of `rm` on an unconfigured Unix system is actually to remove the file without confirmation, but (because deletion is irreversible) many systems *alias* the `rm`command to use an option to turn on confirmation. (As you can verify by running `man rm`, this option is `-i`, so in fact `rm` is really `rm -i`.) There are many situations where confirmation is inconvenient, though, such as when you’re deleting a list of files and don’t want to have to confirm each one. This is especially common when using the wildcard `*` introduced in [Section 2.2](https://www.learnenough.com/command-line-tutorial#sec-listing). For example, to remove all the files ending with “.txt” using a single command, *without* having to confirm each one, you can type this:

```
$ rm -f *.txt

```

Here `-f` (for “force”) overrides the implicit `-i` option and removes all files immediately. ([N.B.](https://en.wikipedia.org/wiki/Nota_bene)You are now in a position to understand the command in [Figure 2](https://www.learnenough.com/command-line-tutorial#fig-command_line_command).)

#### [Unix terseness](https://www.learnenough.com/command-line-tutorial#sec-unix_terseness)

One thing you might notice is that the commands in this section and in [Section 2.2](https://www.learnenough.com/command-line-tutorial#sec-listing) are short: instead of `list`, `move`, `copy`, and `remove`, we have `ls`, `mv`, `cp`, and `rm`. Because the former command names are easier to understand and memorize, you may wonder why the actual commands aren’t longer ([Figure 16](https://www.learnenough.com/command-line-tutorial#fig-y_u_no)).

![images/figures/y_u_no](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ui731p1j30dw0afq4s.jpg)

Figure 16: The terseness of Unix commands can be a source of confusion.

The answer is that Unix dates from a time when most computer users logged on to centralized servers over slow connections, and there could be a noticeable delay between the time users pressed a key and the time it appeared on the terminal. For frequently used commands like listing files, the difference between `list` and `ls` or `remove` and `rm` could be significant. As a result, the most commonly used Unix commands tend to be only two or three letters long.Because it makes them more difficult to memorize, this can be a minor inconvenience when learning them, but over a lifetime of command-line use the savings represented by, say, `mv`really add up.

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_manipulating)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Use the `echo` command and the redirect operator `>` to make a file called `foo.txt`containing the text “hello, world”. Then, using the `cp` command, make a copy of `foo.txt` called `bar.txt`. Using the `diff` command, confirm that the contents of both files are the same.
2. By combining the `cat` command and the redirect operator `>`, create a copy of `foo.txt` called `baz.txt` *without* using the `cp` command.
3. Create a file called `quux.txt` containing the contents of `foo.txt` followed by the contents of `bar.txt`. *Hint*: As noted in [Section 2.1.1](https://www.learnenough.com/command-line-tutorial#sec-exercises_redirecting_appending), `cat` can take multiple arguments.
4. How do `rm nonexistent` and `rm -f nonexistent` differ for a nonexistent file?

### [2.4Summary](https://www.learnenough.com/command-line-tutorial#sec-summary_manipulating)

Important commands from this section are summarized in [Table 3](https://www.learnenough.com/command-line-tutorial#table-manipulating_files).

| **Command**      | **Description**                   | **Example**              |
| ---------------- | --------------------------------- | ------------------------ |
| `>`              | Redirect output to filename       | `$ echo foo > foo.txt`   |
| `>>`             | Append output to filename         | `$ echo bar >> foo.txt`  |
| `cat <file>`     | Print contents of file to screen  | `$ cat hello.txt`        |
| `diff <f1> <f2>` | Diff files 1 & 2                  | `$ diff foo.txt bar.txt` |
| `ls`             | List directory or file            | `$ ls hello.txt`         |
| `ls -l`          | List long form                    | `$ ls -l hello.txt`      |
| `ls -rtl`        | Long by reverse modification time | `$ ls -rtl`              |
| `ls -a`          | List all (including hidden)       | `$ ls -a`                |
| `touch <file>`   | Create an empty file              | `$ touch foo`            |
| `mv <old> <new>` | Rename (move) from old to new     | `$ mv foo bar`           |
| `cp <old> <new>` | Copy old to new                   | `$ cp foo bar`           |
| `rm <file>`      | Remove (delete) file              | `$ rm foo`               |
| `rm -f <file>`   | Force-remove file                 | `$ rm -f bar`            |

Table 3: Important commands from [Section 2](https://www.learnenough.com/command-line-tutorial#sec-manipulating_files).

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_summary_manipulating)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

> FRom faireſt creatures we deſire increaſe,That thereby beauties *Roſe* might neuer die,But as the riper ſhould by time deceaſe,His tender heire might beare his memory:But thou contracted to thine owne bright eyes,Feed’ſt thy lights flame with ſelfe ſubſtantiall fewell,Making a famine where aboundance lies,Thy ſelfe thy foe,to thy ſweet ſelfe too cruell:Thou that art now the worlds freſh ornament,And only herauld to the gaudy ſpring,Within thine owne bud burieſt thy content,And tender chorle makſt waſt in niggarding:   Pitty the world,or elſe this glutton be,   To eate the worlds due,by the graue and thee.

Figure 17: A copy-and-pastable version of Shakespeare’s first sonnet ([*cf.*](https://en.wikipedia.org/wiki/Cf.) [Figure 12](https://www.learnenough.com/command-line-tutorial#fig-sonnet_1)).

1. By copying and pasting the text from the [HTML version](https://www.learnenough.com/command-line-tutorial#fig-copy_paste_sonnet_1) of [Figure 17](https://www.learnenough.com/command-line-tutorial#fig-copy_paste_sonnet_1), use `echo` to make a file called `sonnet_1_complete.txt` containing the full (original) text of Shakespeare’s first sonnet. *Hint*: You may recall getting stuck when `echo` was followed by an unmatched double quote ([Section 1.2](https://www.learnenough.com/command-line-tutorial#sec-our_first_command) and [Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble)), as in `echo "`, but in fact this construction allows you to print out a multi-line block of text. Just remember to put a closing quote at the end, and then redirect to a file with the appropriate name. Check that the contents are correct using `cat` ([Figure 14](https://www.learnenough.com/command-line-tutorial#fig-cat)).
2. Type the sequence of commands needed to create an empty file called `foo`, rename it to `bar`, and copy it to `baz`.
3. What is the command to list only the files starting with the letter “b”? *Hint*: Use a wildcard.
4. Remove both `bar` and `baz` using a *single* call to `rm`. *Hint*: If those are the only two files in the current directory that start with the letter “b”, you can use the wildcard pattern from the previous exercise.

## [3Inspecting files](https://www.learnenough.com/command-line-tutorial#sec-inspecting_files)

Having seen how to create and manipulate files, now it’s time to learn how to examine their contents. This is especially important for files too long to fit on a single screen. In particular, we saw starting in [Section 2.1](https://www.learnenough.com/command-line-tutorial#sec-redirecting_and_appending) how to use the `cat` command to dump the file contents to the screen, but this doesn’t work very well for longer files.

*Note*: Important commands from this section are summarized in [Table 5](https://www.learnenough.com/command-line-tutorial#table-inspecting_files).

### [3.1Downloading a file](https://www.learnenough.com/command-line-tutorial#sec-downloading_a_file)

To give us a place to start, rather than creating a long file by hand (which is cumbersome) we’ll download a file from the Internet using the powerful `curl` utility (sometimes written as “cURL”), which allows us to interact with a URL[17](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-17) at the command line. Although it’s not part of the core Unix command set, the `curl` command is widely available on Unix systems. To make sure it’s available on your system, we can use the `which` command, which looks to see if the given program is available at the command line.[18](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-18) The way to use it is to type `which` followed by the name of the program—in this case, `curl`:

```
$ which curl
/usr/bin/curl

```

I’ve shown the output on my system (`/usr/bin/curl`, usually read as “user bin curl”), but the result on your system may differ. In particular, if the result is just a blank line, you will have to install `curl`, which you can do by Googling for “install curl” followed by the name of your operating system.

Once `curl` is installed, we can download a file called `sonnets.txt` containing a large corpus of text using the command in [Listing 10](https://www.learnenough.com/command-line-tutorial#code-curl).[19](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-19)

Listing 10: Using `curl` to download a longer file.

```
$ curl -OL cdn.learnenough.com/sonnets.txt
$ ls -rtl

```

Be sure to copy the command exactly; in particular, note that the option `-OL` contains a capital letter “O” (`O`) and not a zero (`0`). (Figuring out what these options do is left as an exercise ([Section 3.5.1](https://www.learnenough.com/command-line-tutorial#sec-exercises_inspecting)).) Also, on some systems (for mysterious reasons) you might have to run the command twice to get it to work; by inspecting the results of `ls -rtl`, you should be able to tell if the initial call to `curl` created the file `sonnets.txt` as expected. (If you do have to repeat the `curl` command, you could press up arrow twice to retrieve it, but see [Box 9](https://www.learnenough.com/command-line-tutorial#aside-repeating_commands) for alternatives.)

The result of running [Listing 10](https://www.learnenough.com/command-line-tutorial#code-curl) is `sonnets.txt`, a file containing all 154 of Shakespeare’s sonnets. This file contains 2620 lines, far too many to fit on one screen. Learning how to inspect its contents is the goal of the rest of this section. (Among other things, we’ll learn how to determine that it has 2620 lines without counting them all by hand.)

> Box 9. Repeating previous commands
>
> Repeating previous commands is a frequent task when using the command line. So far in this tutorial, we’ve used the up-arrow key to retrieve (and possibly edit) previous commands, but this isn’t the only possibility. An even quicker way to find and immediately run a previous command involves using the exclamation point `!`, which in the context of software development is usually pronounced “bang”. To run the previous command exactly as written, we can use “bang bang”:
>
> ```
>  $ echo "foo"
>  foo
>  $ !!
>  echo "foo"
>  foo
> ```
>
> A closely related usage is “bang” followed by some number of characters, which runs the last command that started with those characters. For example, to run the last `curl`command, we could type this:
>
> ```
>  $ !curl
> ```
>
> This would save us the trouble of typing out the options, the URL, etc. Depending on our history of commands, the even terser `!cu` or `!c` would work as well. This technique is especially useful when the desired command last happened many commands ago, which can make hitting up arrow cumbersome.
>
> A second and incredibly powerful technique is `⌃R`, which lets you search interactively through your previous commands, and then optionally edit the result before executing.For example, we could try this to bring up the last `curl` command:
>
> ```
>  $ <⌃R>
>  (reverse-i-search)`': curl
> ```
>
> On most systems, hitting return would then put the last `curl` command after our prompt and allow us to edit it (if desired) before hitting return to execute it. When your workflow happens to involve repeatedly running a variety of similar commands, sometimes it can seem like “all commands start with `⌃R`.”
>

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_downloading)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Use the command `curl -I https://www.learnenough.com/` to fetch the *HTTP header* for the Learn Enough website. What is the [HTTP status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) for the address? How does this differ from the status code for `learnenough.com` (without the `https://`)?
2. Using `ls`, confirm that `sonnets.txt` exists on your system. How big is it in bytes?*Hint*: Recall from [Section 2.2](https://www.learnenough.com/command-line-tutorial#sec-listing) that the “long form” of `ls` displays a byte count.
3. The byte count in the previous exercise is high enough that it’s more naturally thought of in *kilobytes* (often treated as 1000 bytes, but actually equal to 210=1024210=1024 bytes). By adding `-h` (“human-readable”) option to `ls`, list the long form of the sonnets file with a human-readable byte count.
4. Suppose you wanted to list the files and directories using **h**uman-readable byte counts, **a**ll, by **r**everse **t**ime-sorted **l**ong-form. What command would you use? Why might this command be the personal favorite of the author of this tutorial?[20](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-20)

### [3.2Making heads and tails of it](https://www.learnenough.com/command-line-tutorial#sec-making_heads_and_tails)

Two complementary commands for inspecting files are `head` and `tail`, which respectively allow us to view the beginning (head) and end (tail) of the file. The `head` command shows the first 10 lines of the file ([Listing 11](https://www.learnenough.com/command-line-tutorial#code-head)).

Listing 11: Looking at the head of the sample text file.

```
$ head sonnets.txt
Shake-speare's Sonnets

I

From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
But as the riper should by time decease,
His tender heir might bear his memory:
But thou contracted to thine own bright eyes,
Feed'st thy light's flame with self-substantial fuel

```

Similarly, `tail` shows the last 10 lines of the file ([Listing 12](https://www.learnenough.com/command-line-tutorial#code-tail)).

Listing 12: Looking at the tail of the sample text file.

```
$ tail sonnets.txt
The fairest votary took up that fire
Which many legions of true hearts had warm'd;
And so the general of hot desire
Was, sleeping, by a virgin hand disarm'd.
This brand she quenched in a cool well by,
Which from Love's fire took heat perpetual,
Growing a bath and healthful remedy,
For men diseas'd; but I, my mistress' thrall,
 Came there for cure and this by that I prove,
 Love's fire heats water, water cools not love.

```

These two commands are useful when (as is often the case) you know for sure you only need to inspect the beginning or end of a file.

#### [Wordcount and pipes](https://www.learnenough.com/command-line-tutorial#sec-wordcount_and_pipes)

By the way, I didn’t recall offhand how many lines `head` and `tail` show by default. Since there are only 10 lines in the output, I could have counted them by hand, but in fact I was able to figure it out using the `wc` command (short for “wordcount”; recall [Figure 16](https://www.learnenough.com/command-line-tutorial#fig-y_u_no)).

The most common use of `wc` is on full files. For example, we can run `sonnets.txt` through `wc`:

```
$ wc sonnets.txt
  2620  17670  95635 sonnets.txt

```

Here the three numbers indicate how many lines, words, and bytes there are in the file, so there are 2620 lines (thereby fulfilling the promise made at the end of [Section 3.1](https://www.learnenough.com/command-line-tutorial#sec-downloading_a_file)), 17670 words, and 95635 bytes.

You are now in a position to be able to guess one method for determining how many lines are in `head sonnets.txt`. In particular, we can combine `head` with the redirect operator ([Section 2.1](https://www.learnenough.com/command-line-tutorial#sec-redirecting_and_appending)) to make a file with the relevant contents, and then run `wc` on it, as shown in [Listing 13](https://www.learnenough.com/command-line-tutorial#code-head_redirected).

Listing 13: Redirecting `head` and running `wc` on the result.

```
$ head sonnets.txt > sonnets_head.txt
$ wc sonnets_head.txt
   10   46   294 sonnets_head.txt

```

We see from [Listing 13](https://www.learnenough.com/command-line-tutorial#code-head_redirected) that there are 10 lines in `head wc` (along with 46 words and 294 bytes).The same method, of course, would work for `tail`.

On the other hand, you might get the feeling that it’s a little unclean to make an intermediate file just to run `wc` on it, and indeed there’s a way to avoid it using a technique called *pipes*.[Listing 14](https://www.learnenough.com/command-line-tutorial#code-head_pipe) shows how to do it.

Listing 14: Piping the result of `head` through `wc`.

```
$ head sonnets.txt | wc
   10   46   294

```

The command in [Listing 14](https://www.learnenough.com/command-line-tutorial#code-head_pipe) runs `head sonnets.txt` and then *pipes* the result through `wc`using the pipe symbol `|` (Shift-backslash on most QWERTY keyboards). The reason this works is that the `wc` command, in addition to taking a filename as an argument, can (like many Unix programs) take input from “standard in” (compare to “standard out” mentioned in [Section 1.2](https://www.learnenough.com/command-line-tutorial#sec-our_first_command)), which in this case is the output of `head sonnets.txt` shown in [Listing 11](https://www.learnenough.com/command-line-tutorial#code-head). The `wc` program takes this input and counts it the same way it counts a file, yielding the same line, word, and byte counts as [Listing 13](https://www.learnenough.com/command-line-tutorial#code-head_redirected).

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_head_tails)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. By piping the results of `tail sonnets.txt` through `wc`, confirm that (like `head`) the `tail` command outputs 10 lines by default.
2. By running `man head`, learn how to look at the first `n` lines of the file. By experimenting with different values of `n`, find a `head` command to print out just enough lines to display the first sonnet in its entirety ([Figure 12](https://www.learnenough.com/command-line-tutorial#fig-sonnet_1)).
3. Pipe the results of the previous exercise through `tail` (with the appropriate options) to print out *only* the 14 lines composing Sonnet 1. *Hint*: The command will look something like `head -n <i> sonnets.txt | tail -n <j>`, where `<i>` and `<j>` represent the numerical arguments to the `-n` option.
4. One of the most useful applications of `tail` is running `tail -f` to view a file that’s actively changing. This is especially common when monitoring files used to log the activity of, e.g., web servers, a practice known as “[tailing the log file](https://en.wikipedia.org/wiki/Tail_(Unix)#File_monitoring)”. To simulate the creation of a log file, run `ping learnenough.com > learnenough.log` in one terminal tab. (The `ping` command “pings” a server to see if it’s working.) In a second tab, type the command to tail the log file. (At this point, both tabs will be stuck, so once you’ve gotten the gist of `tail -f` you should use the technique from [Box 4](https://www.learnenough.com/command-line-tutorial#aside-getting_out_of_trouble) to get out of trouble.)

### [3.3Less is more](https://www.learnenough.com/command-line-tutorial#sec-less_is_more)

Unix provides two utilities for the common task of wanting to look at more than just the head or tail of a file. The older of these programs is called `more`, but (I’d guess initially as a tongue-in-cheek joke) there’s a more powerful variant called `less`.[21](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-21) The `less` program is interactive, so it’s hard to capture in print, but here’s roughly what it looks like:

```
$ less sonnets.txt
Shake-speare's Sonnets

I

From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
But as the riper should by time decease,
His tender heir might bear his memory:
But thou contracted to thine own bright eyes,
Feed'st thy light's flame with self-substantial fuel,
Making a famine where abundance lies,
Thy self thy foe, to thy sweet self too cruel:
Thou that art now the world's fresh ornament,
And only herald to the gaudy spring,
Within thine own bud buriest thy content,
And tender churl mak'st waste in niggarding:
 Pity the world, or else this glutton be,
 To eat the world's due, by the grave and thee.

II

When forty winters shall besiege thy brow,
And dig deep trenches in thy beauty's field,
sonnets.txt

```

The point of `less` is that it lets you navigate through the file in several useful ways, such as moving one line up or down with the arrow keys, pressing space bar to move a page down, pressing `⌃F` to move forward a page (i.e., the same as spacebar) or `⌃B` to move back a page. To quit `less`, type `q` (for “quit”).

![images/figures/tudor_rose](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uid9apdj30af0afgol.jpg)

Figure 18: A [famous rose](https://en.wikipedia.org/wiki/Tudor_rose) from the time of Shakespeare.

Perhaps the most powerful aspect of `less` is the forward slash key `/`, which lets you search through the file from beginning to end. For example, suppose we wanted to search through `sonnets.txt` for “rose” ([Figure 18](https://www.learnenough.com/command-line-tutorial#fig-tudor_rose)),[22](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-22) one of the most frequently used images used in the *Sonnets*.[23](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-23) The way to do this in `less` is to type `/rose` (read “slash rose”), as shown in [Listing 15](https://www.learnenough.com/command-line-tutorial#code-rose_search).

Listing 15: Searching for the string “rose” using `less`.

```
Shake-speare's Sonnets

I

From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
But as the riper should by time decease,
His tender heir might bear his memory:
But thou contracted to thine own bright eyes,
Feed'st thy light's flame with self-substantial fuel,
Making a famine where abundance lies,
Thy self thy foe, to thy sweet self too cruel:
Thou that art now the world's fresh ornament,
And only herald to the gaudy spring,
Within thine own bud buriest thy content,
And tender churl mak'st waste in niggarding:
 Pity the world, or else this glutton be,
 To eat the world's due, by the grave and thee.

II

When forty winters shall besiege thy brow,
And dig deep trenches in thy beauty's field,
/rose

```

The result of pressing return after typing `/rose` in [Listing 15](https://www.learnenough.com/command-line-tutorial#code-rose_search) is to highlight the first occurrence of “rose” in the file. You can then press `n` to navigate to the next match, or `N` to navigate to the previous match.

The last two essential `less` less commands are `G` to move to the end of the file and `1G` (that’s `1` followed by `G`) to move back to the beginning. [Table 4](https://www.learnenough.com/command-line-tutorial#table-less_commands) summarizes what are in my view the most important key combinations (i.e., the ones I think you need to be *dangerous*), but if you’re curious you can find a longer list of commands at the [Wikipedia page on `less`](https://en.wikipedia.org/wiki/Less_(Unix)).

I encourage you to get in the habit of using `less` as your go-to utility for looking at the contents of a file. The skills you develop have other applications as well; for example, the man pages ([Section 1.3](https://www.learnenough.com/command-line-tutorial#sec-man_pages)) use the same interface as `less`, so by learning about `less` you’ll get better at navigating the man pages as well.

| **Command**            | **Description**                | **Example** |
| ---------------------- | ------------------------------ | ----------- |
| `up & down arrow keys` | Move up or down one line       |             |
| `spacebar`             | Move forward one page          |             |
| `⌃F`                   | Move forward one page          |             |
| `⌃B`                   | Move back one page             |             |
| `G`                    | Move to end of file            |             |
| `1G`                   | Move to beginning of file      |             |
| `/<string>`            | Search file for string         | `/rose`     |
| `n`                    | Move to next search result     |             |
| `N`                    | Move to previous search result |             |
| `q`                    | Quit `less`                    |             |

Table 4: The most important `less` commands.

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_summary_less)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Run `less` on `sonnets.txt`. Go down three pages and then back up three pages. Go to the end of the file, then to the beginning, then quit.
2. Search for the string “All” (case-sensitive). Go forward a few occurrences, then back a few occurrences. Then go to the beginning of the file and count the occurrences by searching forward until you hit the end. Compare your count to the result of running `grep All sonnets.txt | wc`. (We’ll learn about `grep` in [Section 3.4](https://www.learnenough.com/command-line-tutorial#sec-grepping).)
3. Using `less` and `/` (“slash”), find the sonnet that begins with the line “Let me not”. Are there any other occurrences of this string in the *Sonnets*? *Hint*: Press `n` to find the next occurrence (if any). *Extra credit*: [Listen to the sonnet](https://youtu.be/bt7OynPUIY8) in both modern and [original pronunciation](http://originalpronunciation.com/). Which version’s rhyme scheme is better?
4. Because `man` uses `less`, we are now in a position to search man pages interactively. By searching for the string “sort” in the man page for `ls`, discover the option to sort files by size. What is the command to display the long form of files sorted so the largest files appear at the bottom? *Hint*: Use `ls -rtl` as a model.

### [3.4Grepping](https://www.learnenough.com/command-line-tutorial#sec-grepping)

One of the most powerful tools for inspecting file contents is `grep`, which probably stands for something, but it’s not important what.[24](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-24) Indeed, *grep* is frequently used as a verb, as in “You should totally grep that file.”

The most common use of `grep` is just to search for a substring in a file. For example, we saw in [Section 3.3](https://www.learnenough.com/command-line-tutorial#sec-less_is_more) how to use `less` to search for the string “rose” in Shakespeare’s sonnets. Using `grep`, we can find the references directly, as shown in [Listing 16](https://www.learnenough.com/command-line-tutorial#code-grep_rose).

Listing 16: Finding the occurrences of “rose” in Shakespeare’s sonnets.

```
$ grep rose sonnets.txt
The rose looks fair, but fairer we it deem
As the perfumed tincture of the roses.
Die to themselves. Sweet roses do not so;
Roses of shadow, since his rose is true?
Which, like a canker in the fragrant rose,
Nor praise the deep vermilion in the rose;
The roses fearfully on thorns did stand,
 Save thou, my rose, in it thou art my all.
I have seen roses damask'd, red and white,
But no such roses see I in her cheeks;

```

With the command in [Listing 16](https://www.learnenough.com/command-line-tutorial#code-grep_rose), it appears that we are in a position to count the number of lines containing references to the word “rose” by piping to `wc` (as in [Section 3.3](https://www.learnenough.com/command-line-tutorial#sec-less_is_more)), as shown in [Listing 17](https://www.learnenough.com/command-line-tutorial#code-grep_rose_wc).

Listing 17: Piping the results of `grep` to `wc`.

```
$ grep rose sonnets.txt | wc
   10   82   419

```

[Listing 17](https://www.learnenough.com/command-line-tutorial#code-grep_rose_wc) tells us that 10 lines contain “rose” (or “roses”, since “rose” is a substring of “roses”).But you may recall from [Figure 12](https://www.learnenough.com/command-line-tutorial#fig-sonnet_1) that Shakespeare’s first sonnet contains “Rose” with a *capital*“R”. Referring to [Listing 16](https://www.learnenough.com/command-line-tutorial#code-grep_rose), we see that this line has in fact been missed. This is because `grep`is case-sensitive by default, and “rose” doesn’t match “Rose”.

As you might suspect, `grep` has an option to perform case-insensitive matching as well. One way to figure it out is to search through the `man` page for `grep`:

- Type `man grep`
- Type `/case` and then return
- Read off the result ([Figure 19](https://www.learnenough.com/command-line-tutorial#fig-man_grep))

(As noted briefly in [Section 1.3](https://www.learnenough.com/command-line-tutorial#sec-man_pages), the man pages use the same interface as the `less` command we met in [Section 3.3](https://www.learnenough.com/command-line-tutorial#sec-less_is_more), so we can search through them using `/`.)

![images/figures/man_grep](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uifwca3j30jg0f6aee.jpg)

Figure 19: The result of searching `man grep` for “case”.

Applying the result of the above procedure yields [Listing 18](https://www.learnenough.com/command-line-tutorial#code-grep_i_wc). Comparing the results of [Listing 18](https://www.learnenough.com/command-line-tutorial#code-grep_i_wc)with [Listing 17](https://www.learnenough.com/command-line-tutorial#code-grep_rose_wc), we see that we now have 12 matching lines instead of only 10, so there must be a total of 12−10=212−10=2 lines containing “Rose” (but not “rose”) in the *Sonnets*.[25](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-25)

Listing 18: Doing a case-insensitive grep.

```
$ grep -i rose sonnets.txt | wc
   12   96   508

```

The `grep` utility is insanely powerful, especially when combined with so-called *regular expressions*, but learning `grep` and `grep -i` are *almost* enough to be dangerous (including the important application of *grepping processes* ([Box 10](https://www.learnenough.com/command-line-tutorial#aside-ps_aux))). We’ll see the third and final `grep`variant needed to be dangerous in [Section 4](https://www.learnenough.com/command-line-tutorial#sec-directories).

> Box 10. Grepping processes
>
> One of the many uses of `grep` is filtering the Unix *process list* for running programs that match a particular string. (On Unix-like systems such as Linux and macOS, user and system tasks each take place within a well-defined container called a *process*.) This is especially useful when there’s a rogue process on your system that needs to be killed. (A good way to find such processes is by running the `top` command, which shows the processes consuming the most resources.)
>
> For example, at one point in the [*Ruby on Rails Tutorial* book](http://railstutorial.org/book), it’s important to eliminate a program called `spring` from the process list. To do this, first the processes need to be found, and the way to see all the processes on your system is to use the `ps` command with the `aux` options:
>
> ```
>  $ ps aux
> ```
>
> Per [Figure 16](https://www.learnenough.com/command-line-tutorial#fig-y_u_no), `ps` is short for “process status”. And for [confusing and obscure reasons](http://www.freebsd.org/cgi/man.cgi?query=ps&manpath=SuSE+Linux/i386+11.3), options to `ps` aren’t written with a dash (so it’s `ps aux` instead of `ps -aux`). (How on earth are you supposed to know this? That’s what this tutorial is for.)
>
> To filter the processes by program name, you pipe the results of `ps` through the `grep`:
>
> ```
>  $ ps aux | grep spring
>  ubuntu 12241 0.3 0.5 589960 178416 ? Ssl Sep20 1:46
>  spring app | sample_app | started 7 hours ago
> ```
>
> The result shown gives some details about the process, but the most important thing is the first number, which is the *process id*, or pid (often pronounced to rhyme with “kid”). To eliminate an unwanted process, we use the `kill` command to issue the Unix terminate code (which [happens to be 15](https://en.wikipedia.org/wiki/Unix_signal#List_of_signals)) to the pid:
>
> ```
>  $ kill -15 12241
> ```
>
> This is the technique I recommend for killing individual processes, such as a rogue web server (with the pid found via `ps aux | grep server`), but sometimes it’s convenient to kill all the processes matching a particular process name, such as when you want to kill all the `spring` processes gunking up your system. In this case, you can kill all the processes with name `spring` using the `pkill` command as follows:
>
> ```
>  $ pkill -15 -f spring
> ```
>
> Any time something isn’t behaving as expected, or a process appears to be frozen, it’s a good idea to run `top` or `ps aux` to see what’s going on, pipe `ps aux` through `grep`to select the suspected processes, and then run `kill -15 <pid>` or `pkill -15 -f <name>` to clear things up.
>

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_grep)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. By searching `man grep` for “line number”, construct a command to find the line numbers in `sonnets.txt` where the string “rose” appears.
2. You should find that the last occurrences of “rose” is (via “roses”) on line 2203. Figure out how to go directly to this line when running `less sonnets.txt`. *Hint*: Recall from [Table 4](https://www.learnenough.com/command-line-tutorial#table-less_commands) that `1G` goes to the top of the file, i.e., line 1. Similarly, `17G` goes to line 17. Etc.
3. By piping the output of `grep` to `head`, print out the first (and *only* the first) line in `sonnets.txt` containing “rose”. *Hint*: Use the result of the second exercise in [Section 3.2.2](https://www.learnenough.com/command-line-tutorial#sec-exercises_head_tails).
4. In [Listing 18](https://www.learnenough.com/command-line-tutorial#code-grep_i_wc), we saw two additional lines that case-insensitively matched “rose”. Execute a command confirming that both of the lines contain the string “Rose” (and not, e.g., “rOSe”). *Hint*: Use a case-sensitive `grep` for “Rose”.
5. You should find in the previous exercise that there are *three* lines matching “Rose” instead of the two you might have expected from [Listing 18](https://www.learnenough.com/command-line-tutorial#code-grep_i_wc). This is because there is one line that contains both “Rose” *and* “rose”, and thus shows up in both `grep rose` and `grep -i rose`. Write a command confirming that the number of lines matching “Rose” but *not* matching “rose” is equal to the expected 2. *Hint*: Pipe the result of `grep` to `grep -v`, and then pipe that result to `wc`. (What does `-v` do? Read the man page for `grep`([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)).)

### [3.5Summary](https://www.learnenough.com/command-line-tutorial#sec-summary_inspecting)

Important commands from this section are summarized in [Table 5](https://www.learnenough.com/command-line-tutorial#table-inspecting_files).

| **Command**                | **Description**                  | **Example**             |
| -------------------------- | -------------------------------- | ----------------------- |
| `curl`                     | Interact with URLs               | `$ curl -O example.com` |
| `which`                    | Locate a program on the path     | `$ which curl`          |
| `head <file>`              | Display first part of file       | `$ head foo`            |
| `tail <file>`              | Display last part of file        | `$ tail bar`            |
| `wc <file>`                | Count lines, words, bytes        | `$ wc foo`              |
| `cmd1 | cmd2`              | Pipe `cmd1` to `cmd2`            | `$ head foo | wc`       |
| `ping <url>`               | Ping a server URL                | `$ ping google.com`     |
| `less <file>`              | View file contents interactively | `$ less foo`            |
| `grep <string> <file>`     | Find string in file              | `$ grep foo bar.txt`    |
| `grep -i <string> <file>`  | Find case-insensitively          | `$ grep -i foo bar.txt` |
| `ps`                       | Show processes                   | `$ ps aux`              |
| `top`                      | Show processes (sorted)          | `$ top`                 |
| `kill -<level> <pid>`      | Kill a process                   | `$ kill -15 24601`      |
| `pkill -<level> -f <name>` | Kill matching processes          | `$ pkill -15 -f spring` |

Table 5: Important commands from [Section 3](https://www.learnenough.com/command-line-tutorial#sec-inspecting_files).

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_inspecting)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. The `history` command prints the history of commands in a particular terminal shell (subject to some limit, which is typically large). Pipe `history` to `less` to examine your command history. What was your 17th command?
2. By piping the output of `history` to `wc`, count how many commands you’ve executed so far.
3. One use of `history` is to grep your commands to find useful ones you’ve used before, with each command preceded by the corresponding number in the command history. By piping the output of `history` to `grep`, determine the number for the last occurrence of `curl`.
4. In [Box 9](https://www.learnenough.com/command-line-tutorial#aside-repeating_commands), we learned about `!!` (“bang bang”) to execute the previous command.Similarly, `!n` executes command number `n`, so that, e.g., `!17` executes the 17th command in the command history. Use the result from the previous exercise to re-run the last occurrence of `curl`.
5. What do the `O` and `L` options in [Listing 10](https://www.learnenough.com/command-line-tutorial#code-curl) mean? *Hint*: Pipe the output of `curl -h` to `less` and search first for the string `-O` and then for the string `-L`.

## [4Directories](https://www.learnenough.com/command-line-tutorial#sec-directories)

Having examined many of Unix utilities for dealing with files, the time has come to learn about *directories*, sometimes known by the synonym *folders* ([Figure 20](https://www.learnenough.com/command-line-tutorial#fig-directory_folder)). As we’ll see, many of the ideas developed in the context of files also apply to directories, but there are many differences as well.

*Note*: Important commands from this section are summarized in [Table 6](https://www.learnenough.com/command-line-tutorial#table-directories).

### [4.1Directory structure](https://www.learnenough.com/command-line-tutorial#sec-structure)

The structure of Unix-style directories is typically indicated using a list of directory names separated by forward slashes, which we can combine with the `ls` command ([Section 2.2](https://www.learnenough.com/command-line-tutorial#sec-listing)) like this:

```
$ ls /Users/mhartl/ruby

```

or like this:

```
$ ls /usr/local/bin

```

As seen in [Figure 20](https://www.learnenough.com/command-line-tutorial#fig-directory_folder), these representations correspond to directories in a hierarchical filesystem, with (say) `mhartl` a subdirectory of `Users` and `ruby` a subdirectory of `mhartl`.

![images/figures/directory_folder](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uin4vlhj30jg09kjuq.jpg)

Figure 20: The correspondence between folders & directories.

Conventions vary when speaking about directories: a *user directory* like `/Users/mhartl` would probably be read as “slash users slash mhartl” or “slash users mhartl”, whereas omitting the initial slash in spoken language is common for *system directories* such as `/usr/local/bin`, which would probably be pronounced “user local bin”. Because *all* Unix directories are ultimately subdirectories of the *root directory* `/` (pronounced “slash”), the leading and separator slashes are implied. *Note*: Referring to forward slashes incorrectly as “backslashes” is a [cause of suffering](https://m.xkcd.com/727/), and should be strictly avoided.

The most important directory for a particular user is the *home directory*, which on my macOS system is `/Users/mhartl`, corresponding to my username (`mhartl`). The home directory can be specified as an *absolute path*, as in `/Users/mhartl`, or using the shorthand for the home directory is the tilde character `~` (which is typed using Shift-backtick, located just to the left of the number 1 on most keyboards). As a result, the two paths shown in [Figure 20](https://www.learnenough.com/command-line-tutorial#fig-directory_folder) are identical: `/Users/mhartl/ruby/projects` is the same as `~/ruby/projects`. (Amusingly, the reason the tilde character is used for the home directory is simply because the “Home” key was the same as the key for producing “~” on [some early keyboards](http://unix.stackexchange.com/questions/34196/why-was-chosen-to-represent-the-home-directory).)

In addition to user directories, every Unix system has *system directories* for the programs essential for the computer’s normal operation. Modifying system files or directories requires special powers granted only to the *superuser*, known as `root`. (This use of “root” is unrelated to the “root directory” mentioned above.) The superuser is so powerful that it’s considered bad form to log in as `root`; instead, tasks executed as `root` should typically use the `sudo`command ([Box 11](https://www.learnenough.com/command-line-tutorial#aside-sudo)).[26](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-26)

> Box 11. “`sudo` make me a sandwich.”
>
> `sudo` gives ordinary users the power to execute commands as the superuser. For example, let’s try `touch`ing a file in the system directory `/opt` as follows:
>
> ```
>  $ touch /opt/foo
>  touch: /opt/foo: Permission denied
> ```
>
> Because normal users don’t have permission to modify `/opt`, the command fails, but it succeeds with `sudo`:
>
> ```
>  $ sudo touch /opt/foo
>  Password:
> ```
>
> As shown, after entering `sudo` we are prompted to enter our user password; if entered correctly, and if the user has been configured to have `sudo` privileges (which is the default on most desktop Unix systems), then the command will succeed. As shown in [Figure 21](https://www.learnenough.com/command-line-tutorial#fig-sandwich), this pattern of being denied at first, only to succeed using `sudo`, is a common theme in computing.
>
> To check that the file really was created, we can `ls` it:
>
> ```
>  $ ls -l /opt/foo
>  -rw-r--r-- 1 root wheel 0 Jul 23 19:13 /opt/foo
> ```
>
> Note that (1) a normal user can `ls` a file in a system directory (without `sudo`) and (2) the name `root` appears in the listing, indicating that the superuser owns the file. (The meaning of the second term, `wheel`, is a little obscure, but you can learn about it on a site called, appropriately enough, [superuser](http://superuser.com/questions/191955/what-is-the-wheel-user-in-os-x).)
>
> To remove the file we just created, we again need superuser status:
>
> ```
>  $ rm -f /opt/foo
>  rm: /opt/foo: Permission denied
>  $ sudo !!
>  $ !ls
>  ls: /opt/foo: No such file or directory
> ```
>
> Here the first `rm` fails, so we’ve run `sudo !!`, which runs `sudo` and then the previous command , and we’ve followed that up with `!ls`, which runs the previous `ls` command ([Box 9](https://www.learnenough.com/command-line-tutorial#aside-repeating_commands)).
>
> It’s also worth noting the English pronunciation of something like `sudo !!`, which is important when communicating via spoken language. As noted in [Box 9](https://www.learnenough.com/command-line-tutorial#aside-repeating_commands), `!!` is pronounced “bang bang”. `sudo`, meanwhile, is pronounced either “SOO-doo” or “SOO-doh”. Both pronunciations are common, though I prefer the former because the `do` in `sudo` is in fact just the English word “do”. Thus, my preferred pronunciation for `sudo !!` is “SOO-doo bang bang”.
>
> By the way, the `su` in `sudo` [originally stood](https://pthree.org/2009/12/31/the-meaning-of-su/) for “super-user”, but over time its use expanded, and now is usually thought of as “substitute user”. `sudo` is therefore a contraction of “substitute user do”, with the substitute user being the superuser by default. Because the superuser can do anything, the command “sudo make me a sandwich” in [Figure 21](https://www.learnenough.com/command-line-tutorial#fig-sandwich) succeeds when a mere “make me a sandwich” does not.
>

![images/figures/sandwich](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uiv0fl1j30a008bjrf.jpg)

Figure 21: “[Sandwich](https://m.xkcd.com/149/)” (via [xkcd](http://xkcd.com/)) derives humor from the behavior of `sudo`.

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_structure)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Write in words how you might speak the directory `~/foo/bar`.
2. In `/Users/bill/sonnets`, what is the home directory? What is the username? Which directory is deepest in the hierarchy?
3. For a user with username `bill`, how do `/Users/bill/sonnets` and `~/sonnets`differ (if at all)?

### [4.2Making directories](https://www.learnenough.com/command-line-tutorial#sec-making_directories)

So far in this tutorial, we’ve created (and removed) a large number of text files. The time has finally come to make a directory to contain them. Although most modern operating systems include a graphical interface for this task, the Unix way to do it is with `mkdir` (short for “make directory”, per [Figure 16](https://www.learnenough.com/command-line-tutorial#fig-y_u_no)):

```
$ mkdir text_files

```

Having made the directory, we can move the text files there using a wildcard:

```
$ mv *.txt text_files/

```

We can confirm the move worked by listing the directory:

```
$ ls text_files/
sonnet_1.txt     sonnet_1_reversed.txt sonnets.txt

```

(Depending on how closely you’ve followed this tutorial, your results may vary.)

By default, running `ls` on a directory shows its *contents*, but we can show just the directory using the `-d` option:

```
$ ls -d text_files/
text_files/

```

This usage is especially common with the `-l` option ([Section 2.2](https://www.learnenough.com/command-line-tutorial#sec-listing)):

```
$ ls -ld text_files/
drwxr-xr-x 7 mhartl staff 238 Jul 24 18:07 text_files

```

Finally, we can change directories using `cd`:

```
$ cd text_files/

```

Note that `cd` typically supports tab completion, so (as described in [Box 8](https://www.learnenough.com/command-line-tutorial#aside-tab_completion)) we can actually type `cd tex⇥`.

After running `cd`, we can confirm that we’re in the correct directory using the “print working directory” command, `pwd`, together with another call to `ls`:

```
$ pwd
/Users/mhartl/text_files
$ ls
sonnet_1.txt     sonnet_1_reversed.txt sonnets.txt

```

These last steps of typing `pwd` to double-check the directory, and especially running `ls` to inspect the directory contents, are a matter of habit for many a grizzled command-line veteran.(Your result for `pwd` will, of course, be different, unless you happen to be using the username “mhartl” on macOS.)

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_making_dirctories)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. What is the option for making intermediate directories as required, so that you can create, e.g., `~/foo` and `~/foo/bar` with a single command? *Hint*: Refer to the man page for `mkdir`.
2. Use the option from the previous exercise to make the directory `foo` and, within it, the directory `bar` (i.e., `~/foo/bar`) with a single command.
3. By piping the output of `ls` to `grep`, list everything in the home directory that contains the letter “o”.

### [4.3Navigating directories](https://www.learnenough.com/command-line-tutorial#sec-navigating_directories)

We saw in [Section 4.2](https://www.learnenough.com/command-line-tutorial#sec-making_directories) how to use `cd` to change to a directory with a given name. This is one of the most common ways of navigating, but there are a couple of special forms worth knowing. The first is changing to the directory one level up in the hierarchy using `cd ..` (read “see-dee dot-dot”):

```
$ pwd
/Users/mhartl/text_files
$ cd ..
$ pwd
/Users/mhartl

```

In this case, because `/Users/mhartl` is my *home directory*, we could have accomplished the same thing using `cd` by itself:

```
$ cd text_files/
$ pwd
/Users/mhartl/text_files
$ cd
$ pwd
/Users/mhartl

```

The reason this works is that `cd` by itself changes to the user’s home directory, wherever that is.This means that

```
$ cd

```

and

```
$ cd ~

```

are equivalent.

When changing directories, it’s frequently useful to be able to specify the home directory somehow. For example, suppose we make a second directory and cd into it:

```
$ pwd
/Users/mhartl
$ mkdir second_directory
$ cd second_directory/

```

Now if we want to change to the `text_files` directory, we can `cd` to `text_files` via the home directory `~`:

```
$ pwd
/Users/mhartl/second_directory
$ cd ~/text_files
$ pwd
/Users/mhartl/text_files

```

Incidentally, we’re now in a position to understand the prompts shown in [Figure 6](https://www.learnenough.com/command-line-tutorial#fig-command_exercise): I have my prompt configured to show the current directory, which might be something like `[~]`, `[ruby]`, or `[projects]`. (We’ll discuss how to customize the prompt in [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial). Especially eager (or impatient) readers can exercise their technical sophistication ([Box 5](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication)) by [Googling for how to do it](http://lmgtfy.com/?q=bash+customize+prompt).)

Closely related to `..` for “one directory up” is `.` (read “dot”) which means “the current directory”. The most common use of `.` is when moving or copying files to the current directory:

```
$ pwd
/Users/mhartl/text_files
$ cd ~/second_directory
$ ls
$ cp ~/text_files/sonnets.txt .
$ ls
sonnets.txt

```

Note in that the first call to `ls` returns nothing, because `second_directory` is initially empty.

Another common use of `.` is in conjunction with the `find` command, which like `grep` is insanely powerful, but in my own use it looks like this 99% of the time:

```
$ cd
$ find . -name '*.txt'
./text_files/sonnet_1.txt
./text_files/sonnet_1_reversed.txt
./text_files/sonnets.txt

```

In words, what this does is find files whose names match the pattern `*.txt`, starting in the current directory `.` and then in its subdirectories.[27](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-27) The `find` utility is incredibly useful for finding a misplaced file at the command line.

Perhaps my favorite use of `.` is in “open dot”, which will work only on macOS:

```
$ cd ~/ruby/projects
$ open .

```

The remarkable `open` command opens its argument using whatever the default program is for the given file or directory. (A similar command, `xdg-open`, works on some Linux systems.) For example, `open foo.pdf` would open the PDF file with the default viewer (which is Preview on most Macs). In the case of a directory such as `.`, that default program is the Finder, so `open .`produces a result like that shown in [Figure 20](https://www.learnenough.com/command-line-tutorial#fig-directory_folder).

A final navigational command, and one of my personal favorites, is `cd -`, which cds to the *previous* directory, wherever it was:

```
$ pwd
/Users/mhartl/second_directory
$ cd ~/text_files
$ pwd
/Users/mhartl/text_files
$ cd -
/Users/mhartl/second_directory

```

I find that `cd -` is especially useful when combining commands, as described in [Box 12](https://www.learnenough.com/command-line-tutorial#aside-combining_commands).

> Box 12. Combining commands
>
> It’s often convenient to combine commands at the command line, such as when installing software using the Unix programs `configure` and `make`, which often appear in the following sequence:
>
> ```
>  $ ./configure ; make ; make install
> ```
>
> This line runs the `configure` program from the current directory `.`, and then runs both `make` and `make install`. (You are not expected to understand what these programs do, and indeed they won’t work on your system unless you happen to be in the directory of a program designed to be installed this way.) Because they are separated by the semicolon character `;`, three commands are run in sequence.
>
> An even better way to combine commands is with the double-ampersand `&&`:
>
> ```
>  $ ./configure && make && make install
> ```
>
> The difference is that commands separated by `&&` run only if the previous command *succeeded*. In contrast, with `;` all the commands will be run no matter what, which will cause an error in the likely case that subsequent commands depend on the results of the ones that precede them.
>
> I especially like to use `&&` in combination with `cd -`, which lets me do things like this:
>
> ```
>  $ build_article && cd ~/tau && deploy && cd -
> ```
>
> Again, you are not expected to understand these commands, but the general idea is that we can (say) build an article in one directory, `cd` to a different directory, deploy (perhaps a [website](http://tauday.com/)) to production, and then `cd` back (`cd -`) to the original directory, where we can continue our work. Then, if need be, we can just use up arrow (or one of the techniques from [Box 9](https://www.learnenough.com/command-line-tutorial#aside-repeating_commands)) to retrieve the whole thing and do it all again.
>

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_navigating_directories)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. How do the effects of `cd` and `cd ~` differ (or do they)?
2. Change to `text_files`, then change to `second_directory` using the “one directory up” double dot operator `..`.
3. From wherever you are, create an empty file called `nil` in `text_files` using whatever method you wish.
4. Remove `nil` from the previous exercise using a different path from the one you used before. (In other words, if you used the path `~/text_files` before, use something like `../text_files` or `/Users/<username>/text_files`.)

### [4.4Renaming, copying, and deleting directories](https://www.learnenough.com/command-line-tutorial#sec-removing_directories)

The commands for renaming, copying, and deleting directories are similar to those for files ([Section 2.3](https://www.learnenough.com/command-line-tutorial#sec-renaming_copying_deleting)), but there are some subtle differences worth noting. The command with the least difference is `mv`, which works just as it does for files:

```
$ mkdir foo
$ mv foo/ bar/
$ cd foo/
-bash: cd: foo: No such file or directory
$ cd bar/

```

Here the error message indicates that the `mv` worked: there is no file or directory called `foo`.(The word `bash` refers to the shell being run, in this case the “[Bourne Again SHell](https://www.gnu.org/software/bash/)”.) The only minor subtlety is that the trailing slashes (which are typically added automatically by tab completion ([Box 8](https://www.learnenough.com/command-line-tutorial#aside-tab_completion))) are optional:

```
$ cd
$ mv bar foo
$ cd foo/

```

This issue with trailing slashes never makes a difference with `mv`, but with `cp` it can be a source of much confusion. In particular, when copying directories, the behavior you usually want is to copy the directory contents *including* the directory, which on many systems requires leaving off the trailing slash. When copying files, you also need to include the `-r` option (for “recursive”).For example, to copy the contents of the `text_files` directory to a new directory called `foobar`, we use the command shown in [Listing 19](https://www.learnenough.com/command-line-tutorial#code-cp_r).

Listing 19: Copying a directory.

```
$ cd
$ mkdir foobar
$ cd foobar/
$ cp -r ../text_files .
$ ls
text_files

```

Note that we’ve used `..` to make a *relative path*, going up one directory and then into `text_files`. Also note the *lack* of a trailing slash in `cp -r ../text_files .`; if we included it, we’d get [Listing 20](https://www.learnenough.com/command-line-tutorial#code-cp_slash) instead.

Listing 20: Copying with a trailing slash.

```
$ cp -r ../text_files/ .
$ ls
sonnet_1.txt     sonnet_1_reversed.txt sonnets.txt   text_files

```

In other words, [Listing 20](https://www.learnenough.com/command-line-tutorial#code-cp_slash) copies the individual files, but not the directory itself. As a result, I recommend always omitting the trailing slash, as in [Listing 19](https://www.learnenough.com/command-line-tutorial#code-cp_r); if you want to copy only the files, be explicit using the star operator, as in:

```
$ cp ../text_files/* .

```

Unlike renaming (moving) and copying directories, which use the same `mv` and `cp` commands used for files, in the case of removing directories there’s a dedicated command called `rmdir`. In my experience, though, it rarely works, as seen here:

```
$ cd
$ rmdir second_directory
rmdir: second_directory/: Directory not empty

```

The error message here is what happens 99% of the time when I try to remove directories, because `rmdir` requires the directory to be empty. You can of course empty it by hand (using `rm` repeatedly), but this is frequently inconvenient, and I almost always use the more powerful (but *much* more dangerous) “remove recursive force” command `rm -rf`, which removes a directory, its files, and any subdirectories without confirmation ([Listing 21](https://www.learnenough.com/command-line-tutorial#code-rm_rf)).

Listing 21: Using `rm -rf` to remove a directory.

```
$ rm -rf second_directory/
$ ls second_directory
ls: second_directory: No such file or directory

```

As the error message from `ls` in [Listing 21](https://www.learnenough.com/command-line-tutorial#code-rm_rf) indicates (“No such file or directory”), our use of `rm -rf` succeeded in removing the directory.

The powerful command `rm -rf` is too convenient to ignore, but remember: “[With great power comes great responsibility](https://en.wikipedia.org/wiki/Uncle_Ben#.22With_great_power_comes_great_responsibility.22)” ([Figure 22](https://www.learnenough.com/command-line-tutorial#fig-spider_man)).[28](https://www.learnenough.com/command-line-tutorial#cha-0_footnote-28)

![images/figures/spider_man](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uiwi29ej30hs0a00tu.jpg)

Figure 22: This [superhero](https://en.wikipedia.org/wiki/Spider-Man) understands how to use the power of `rm -rf` responsibly.

#### [Grep redux](https://www.learnenough.com/command-line-tutorial#sec-grep_redux)

Now that we know a little about directories, we are in a position to add a useful `grep` variation to our toolkit from [Section 3.4](https://www.learnenough.com/command-line-tutorial#sec-grepping). As with `cp` and `rm`, `grep` takes a “recursive” option, `-r`, which in this case greps through a directory’s files and the files in its subdirectories. This is incredibly useful when you’re looking for a string in a file somewhere in a hierarchy of directories, but you’re not sure where the file is. Here’s the setup, which puts the word “[sesquipedalian](http://dictionary.reference.com/browse/sesquipedalian)” in a file called `long_word.txt`:

```
$ cd text_files/
$ mkdir foo
$ cd foo/
$ echo sesquipedalian > long_word.txt
$ cd

```

The final `cd` puts us back in the home directory. Suppose we now want to find the file containing “sesquipedalian”. The way *not* to do it is this:

```
$ grep sesquipedalian text_files
grep: text_files: Is a directory

```

Here `grep`’s error message indicates that the command didn’t work, but adding `-r` does the trick:

```
$ grep -r sesquipedalian text_files
text_files/foo/long_word.txt:sesquipedalian

```

Because case rarely matters, I recommend making a habit of adding the `-i` option when grepping recursively, as follows:

```
$ grep -ri sesquipedalian text_files
text_files/foo/long_word.txt:sesquipedalian

```

Armed with `grep -ri`, we are now equipped to find strings of our choice in arbitrarily deep hierarchies of directories.

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_mv_cp_rmdir)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Make a directory `foo` with a subdirectory `bar`, then rename the subdirectory to `baz`.
2. Copy all the files in `text_files`, *with* directory, into `foo`.
3. Copy all the files in `text_files`, *without* directory, into `bar`.
4. Remove `foo` and everything in it using a single command.

### [4.5Summary](https://www.learnenough.com/command-line-tutorial#sec-summary_directories)

Important commands from this section are summarized in [Table 6](https://www.learnenough.com/command-line-tutorial#table-directories).

| **Command**               | **Description**                     | **Example**             |
| ------------------------- | ----------------------------------- | ----------------------- |
| `mkdir <name>`            | Make directory with name            | `$ mkdir foo`           |
| `pwd`                     | Print working directory             | `$ pwd`                 |
| `cd <dir>`                | Change to <dir>                     | `$ cd foo/`             |
| `cd ~/<dir>`              | cd relative to home                 | `$ cd ~/foo/`           |
| `cd`                      | Change to home directory            | `$ cd`                  |
| `cd -`                    | Change to previous directory        | `$ cd && pwd && cd -`   |
| `.`                       | The current directory               | `$ cp ~/foo.txt .`      |
| `..`                      | One directory up                    | `$ cd ..`               |
| `find`                    | Find files & directories            | `$ find . -name foo*.*` |
| `cp -r <old> <new>`       | Copy recursively                    | `$ cp -r ~/foo .`       |
| `rmdir <dir>`             | Remove (empty) dir                  | `$ rmdir foo/`          |
| `rm -rf <dir>`            | Remove dir & contents               | `$ rm -rf foo/`         |
| `grep -ri <string> <dir>` | Grep recursively (case-insensitive) | `$ grep -ri foo bar/`   |

Table 6: Important commands from [Section 4](https://www.learnenough.com/command-line-tutorial#sec-directories).

#### [Exercises](https://www.learnenough.com/command-line-tutorial#sec-exercises_summary_directories)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Starting in your home directory, execute a single command-line command to make a directory `foo`, change into it, create a file `bar` with content “baz”, print out `bar`’s contents, and then `cd` back to the directory you came from. *Hint*: Combine the commands as described in [Box 12](https://www.learnenough.com/command-line-tutorial#aside-combining_commands).
2. What happens when you run the previous command again? How many of the commands executed? Why?
3. Explain why the command `rm -rf /` is unbelievably dangerous, and why you should never type it into a terminal window, not even as a joke.
4. How can the previous command be made even more dangerous? *Hint*: Refer to [Box 11](https://www.learnenough.com/command-line-tutorial#aside-sudo).(This command is so dangerous you shouldn’t even *think* it, much less type it.)

## [5Conclusion](https://www.learnenough.com/command-line-tutorial#sec-conclusion)

Congratulations! You’ve officially learned enough command line to be *dangerous*. Of course, this is only one step on a longer journey, both toward command-line excellence ([Box 13](https://www.learnenough.com/command-line-tutorial#aside-additional_resources)) and software development wizardry. As you proceed on this journey, you will probably discover that learning computer magic can be exciting and empowering, but it can also be *hard*. Indeed, you may already have discovered this fact, either on your own or while doing this tutorial. To those brave magicians-in-training who wish to proceed, I offer the following sequence, which is currently in preparation:

1. Developer Fundamentals
   1. [*Learn Enough Command Line to Be Dangerous*](http://www.learnenough.com/command-line-tutorial) (you are here)
   2. [*Learn Enough Text Editor to Be Dangerous*](http://www.learnenough.com/text-editor-tutorial)
   3. [*Learn Enough Git to Be Dangerous*](http://www.learnenough.com/git-tutorial)
2. Web Basics
   1. [*Learn Enough HTML to Be Dangerous*](http://www.learnenough.com/html-tutorial)
   2. [*Learn Enough CSS & Layout to Be Dangerous*](http://www.learnenough.com/css-and-layout-tutorial)
   3. [*Learn Enough JavaScript to Be Dangerous*](http://www.learnenough.com/javascript-tutorial)
3. Intro Ruby Web Development
   1. [*Learn Enough Ruby to Be Dangerous*](http://www.learnenough.com/ruby-tutorial)
   2. [*Learn Enough Sinatra to Be Dangerous*](http://www.learnenough.com/sinatra-tutorial)
   3. [*Learn Enough Ruby on Rails to Be Dangerous*](http://www.learnenough.com/ruby-on-rails-tutorial)
4. Professional Ruby Web Development
   - [*The Ruby on Rails Tutorial*](http://www.railstutorial.org/)

Only the first three titles and the last title in the above list are complete, but all the other links go to landing pages where you can sign up to be notified when the next tutorial in the sequence is ready. See you there!

> Box 13. Additional resources
>
> I recommend following the *Learn Enough* sequence, as it represents the shortest path to technical proficiency and software development skills, but at some point you’ll probably want to expand your command-line skills as well. When that time comes, I recommend consulting this list, which consists mainly of resources recommended by readers of the present tutorial:
>
> - [*Conquering the Command Line*](http://conqueringthecommandline.com/) book and screencasts by Mark Bates (which like the present tutorial is available for free [online](http://conqueringthecommandline.com/book))
> - [edX course on Linux](https://www.edx.org/course/introduction-linux-linuxfoundationx-lfs101x-2)
> - [Codecademy course on the command line](https://www.codecademy.com/learn/learn-the-command-line)
> - The similarly named [*The Command Line Crash Course*](http://cli.learncodethehardway.org/book/) and [*A Command Line Crash Course*](http://www.vikingcodeschool.com/web-development-basics/a-command-line-crash-course)
> - [*Learning the Shell*](http://linuxcommand.org/lc3_learning_the_shell.php)
>
> *Learn Enough Command Line to Be Dangerous*. Copyright © 2015 by Michael Hartl.
>
> If you enjoyed this tutorial, please [leave a review at Amazon](https://www.amazon.com/dp/B01KG84X44). Thanks!
>
