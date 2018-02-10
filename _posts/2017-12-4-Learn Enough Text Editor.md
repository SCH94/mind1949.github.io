---
layout: post
title: "Learn Enought Text Editor"
date: 2017-12-4
tags:
  Learn_Enough
  教材
  Text_Editor
---
[![Cover web](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uoe6v3wj30fg0na75g.jpg)](https://www.learnenough.com/text-editor-tutorial)

# Learn Enough Text Editor to Be Dangerous**Michael Hartl**

**Michael Hartl**

A tutorial introduction to text editors

*Learn Enough Text Editor to Be Dangerous* is designed to help you learn to use what is arguably the most important item in the [aspiring computer magician](http://learnenough.com/command-line#aside-computer_magic)’s bag of tricks: a *text editor*.Learning how to use a text editor is an essential component of [technical sophistication](https://www.learnenough.com/command-line-tutorial#aside-technical_sophistication).

Unlike other text editor tutorials, which are typically tied to a specific editor, this tutorial is designed to introduce the entire *category* of application—a category many people don’t even know exists. Moreover, editor-specific tutorials tend to be aimed at professional developers, and generally assume years of experience, but *Learn Enough Text Editor to Be Dangerous* doesn’t even assume you know what a “text editor” is. Its only prerequisite is a basic understanding of the Unix command line, such as that provided by [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial).[1](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-1) Because *Learn Enough Text Editor to Be Dangerous* is part of a [series of tutorials](http://learnenough.com/#coming_soon)designed to teach the fundamentals of software development (with a particular focus on the prerequisites for learning web development with the [Ruby on Rails Tutorial](http://railstutorial.org/)), it’s ideally suited for anyone who wants to learn the skills necessary to work with developers or to become developers themselves. Finally, even if you already know how to use a text editor, following this tutorial (and doing the exercises) will help fill in any gaps in your knowledge, and you might even learn a few new tricks.

*Note*: To get the most out of this tutorial, join the [Learn Enough Society](http://learnenough.com/story), a subscription service from Learn Enough to Be Dangerous that includes integrated progress tracking, exercise answers, live chat, and streaming videos. See [learnenough.com/story](http://learnenough.com/story) for more information.

Unlike most programs used to produce written documents, such as word processors and email clients, a *text editor* is an application specifically designed to edit *plain text* (often called just “text” for short). Learning to use a text editor is important because text is ubiquitous in modern computing—it’s used for code, markup, configuration files, and many other things.[2](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-2) (Indeed, I’m using plain text to write this very document.) Although it’s surprisingly difficult to define exactly what “plain text” is, from a practical perspective it means that the text itself doesn’t have any formatting, or at least none that matters. There’s no notion of *emphasized* or **boldface** text, the font size and `typeface` don’t matter, etc.—the only thing that does matter is the *content*. For example, although the previous sentence contains formatted output like *this*, its source is plain text, and appears as in [Listing 1](https://www.learnenough.com/text-editor-tutorial#code-html_source).[3](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-3)

Listing 1: The HTML source of a sentence in this tutorial.

```
There's no notion of <em>emphasized</em> or <strong>boldface</strong> text,
the <small>font size</small> and <code>typeface</code> don't matter,
etc.&mdash;the only thing that does matter is the <em>content</em>.

```

In [Listing 1](https://www.learnenough.com/text-editor-tutorial#code-html_source), the desired formatting options are indicated with special *tags* (such as the HTML emphasis tag `<em>…</em>`) rather than by changing the appearance of the text itself.[4](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-4) This is the main reason why the more familiar word processor programs such as Word aren’t well-suited to editing plain text, and a different sort of tool is needed ([Box 1](https://www.learnenough.com/text-editor-tutorial#aside-word_processors)).

> Box 1. Word processors vs. text editors
>
> Even if you’ve never used a text editor, the chances are good that you’ve used a similar tool, a *word processor*. There’s a lot of overlap between the features of word processors and text editors. For example, they both allow you create documents, find and replace or cut/copy/paste text, and save the results. The main difference is that word processors are generally designed to produce documents following the principle of “What You See Is What You Get” (WYSIWYG, pronounced “WIZ-ee-wig”), so that effects such as *emphasis*or **boldface** are achieved directly in the application, instead of with plain-text markup like `<em>emphasis</em>` or `**boldface**`. For the most part, word processors also save their results in proprietary formats that sometimes go bad (as many who’ve tried opening old Word files have learned to their chagrin).
>
> In contrast, text editors are designed to modify plain text, one of the most universal and durable formats. Text editors also differ from word processors in having features aimed at more technical users, including syntax highlighting for source code, automatic indentation, support for [regular expressions](http://learnenough.com/regular-expressions-tutorial), and customization via packages and snippets. A good text editor is thus an essential tool in every technical person’s toolkit.
>

![images/figures/y_u_no_word_processor](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uomgzn9j30dw0dw0to.jpg)

Figure 1: Why not edit plain text with Microsoft Word?

Building on the material developed in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), *Learn Enough Text Editor to Be Dangerous* starts by covering the important *Vim* editor ([Section 1](https://www.learnenough.com/text-editor-tutorial#sec-vim)), which can be run at the command line directly inside a terminal window. Vim will give us a chance to see our first examples of the most important functions of a text editor, but because Vim can be forbiddingly complex for a beginner, in this tutorial we will cover only the bare minimum necessary to make basic edits. The rest of the tutorial will expand on the themes developed in [Section 1](https://www.learnenough.com/text-editor-tutorial#sec-vim) by describing some of the many powerful features required in any programmer-grade text editor, with examples drawn principally from [*Atom*](http://atom.io/), an open-source cross-platform editor, with additional examples from the closely related [Sublime Text](http://www.sublimetext.com/) editor and from [Cloud9](http://c9.io/), a cloud [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment).[5](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-5)

As with [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), this tutorial is part of the *Unix tradition*, which includes virtually every operating system you’ve ever heard of (macOS, iOS, Android, Linux, etc.) except Microsoft Windows. Although all the editors we’ll discuss do run under Windows, using a non-Unix OS introduces friction into the process, so Windows users are strongly encouraged to run a free *Linux virtual machine* (as described in [Box 2](https://www.learnenough.com/text-editor-tutorial#aside-virtual_machine)) in order to get the most out of this tutorial. Another good option is to use a cloud IDE, which comes with a built-in command line and text editor; to go this route, follow the “[Development environment](https://www.railstutorial.org/book/beginning#sec-development_environment)” section in the [*Ruby on Rails Tutorial* book](http://railstutorial.org/book).

> Box 2. Running a virtual machine
>
> In order to complete this tutorial, Windows users should install a couple of free programs to run a *virtual machine* (a simulation of a computer) that allows Windows to host a version of the Linux operating system. The steps appear as follows:
>
> 1. Install the right version of [VirtualBox](https://www.virtualbox.org/) for your system.
> 2. Download the [Learn Enough Virtual Machine](https://softcover-static.s3.amazonaws.com/LearnEnough-v.1.4.ova) (large file).
> 3. Once the download is complete, double-click the resulting “OVA” file and follow the instructions to install the Virtual Machine (VM).
> 4. Double-click the VM itself and log in using the default user’s password, which is “`foobar!`”.
>
> The result will be a Linux desktop environment (including a command-line terminal program and text editor) pre-configured for this tutorial ([Figure 2](https://www.learnenough.com/text-editor-tutorial#fig-virtual_machine)).
>
> In the longer run, I recommend switching to a Mac as soon as possible. (*Warning*: As we’ll discuss later in this tutorial ([Box 5](https://www.learnenough.com/text-editor-tutorial#aside-holy_wars)), this could start a holy war.) You might have to save up a bit, as Macs are generally more expensive than Windows machines, but in most cases the increased productivity will quickly pay for the difference. (If you find yourself liking Linux, feel free to stick with it, but Macs are generally easier to use with a better user interface. Plus, you can always run Linux inside a VM, even on a Mac.)
>

![images/figures/ubuntu_desktop](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uoonnhjj30jg0ay0v9.jpg)

Figure 2: A Linux virtual machine running inside a host OS.

The focus throughout *Learn Enough Text Editor to Be Dangerous* is on general principles, so no matter which editor you end up using, you will have a good mental checklist of the kinds of tasks you should rely on your editor to perform. In addition, because the details vary by particular text editor and by system, this tutorial presents an ideal opportunity to continue developing your *technical sophistication* ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)). Finally, don’t feel any pressure to master everything at once.You can be productive with even a small subset of what’s included in this tutorial. Because technically sophisticated people use text editors practically every day, you’ll keep learning new tricks in perpetuity.

> Box 3. Technical sophistication
>
> The phrase *technical sophistication*, [mentioned before](http://learnenough.com/command-line-tutorial#aside-technical_sophistication) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), refers to the general ability to use computers and other technical things.This includes both existing knowledge (such as familiarity with text editors and the Unix command line) and the ability to acquire *new* knowledge, as illustrated in [Figure 3](https://www.learnenough.com/text-editor-tutorial#fig-tech_support_cheat_sheet). Unlike “hard skills” like coding and version control, this latter aspect of technical sophistication is a “soft skill”—difficult to teach directly, but essential to develop if you want to work with computer programmers or to become a programmer yourself.
>
> In the context of text editors, technical sophistication includes things like reading menu items to figure out what they do, using the Help menu to discover new commands, learning keyboard shortcuts by reading menu items or Googling around, etc. It also involves a tolerance for ambiguity: technically sophisticated readers won’t panic if a tutorial says to use ⌘Z to Undo something when it’s actually ⌃Z on their system. They also won’t panic if they see ⌘Z but don’t know what ⌘ means, because they know they can skim ahead to find something like [Table 2](https://www.learnenough.com/text-editor-tutorial#table-keyboard_symbols), or simply [Google for it](http://lmgtfy.com/?q=mac+special+keys). Perhaps the most important aspect of technical sophistication is an *attitude*—a confidence and can-do spirit in the face of confusion that is well worth cultivating.
>
> Throughout the rest of *Learn Enough Text Editor to Be Dangerous*, we’ll refer back to this box whenever we encounter examples of issues that require a little technical sophistication to solve. With experience, you too will become one of the “computer people” from [Figure 3](https://www.learnenough.com/text-editor-tutorial#fig-tech_support_cheat_sheet)who seem to have the [magical](https://www.learnenough.com/command-line-tutorial#aside-computer_magic) ability to figure out technical things.[6](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-6) (*Warning*: You might need a new [shirt](http://www.thinkgeek.com/product/388b/) ([Figure 4](https://www.learnenough.com/text-editor-tutorial#fig-not_fix_computer)).)
>

![images/figures/tech_support_cheat_sheet](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uos6dx7j30kc0mvq4w.jpg)

Figure 3: “[Tech Support Cheat Sheet](https://m.xkcd.com/627/)” (via [xkcd](http://xkcd.com/)).

![images/figures/not_fix_computer](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uouxxexj30b00bcjtp.jpg)

Figure 4: A [T-shirt](http://www.thinkgeek.com/product/388b/) for the technically sophisticated.

## [1Vim](https://www.learnenough.com/text-editor-tutorial#sec-vim)

The vi (pronounced “vee-eye”) editor dates back to the earliest days of Unix, and Vim (pronounced “vim”) is an updated version that stands for “Vi IMproved”. Vim is absolutely a full-strength text editor, and many developers use it for their daily editing needs, but the barrier to Vim mastery is high, and it requires substantial customization and technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) to reach its full potential. Vim also has a large and often obscure set of commands, which rarely correspond to native keybindings (keyboard shortcuts), making Vim challenging to learn and remember. As a result, I generally recommend beginners learn a “modern” editor ([Section 2](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors)) for everyday use. Nevertheless, I consider a minimal proficiency with Vim to be essential, simply because Vim is utterly ubiquitous—it’s present on virtually every Unix-like system in the known universe, which means that if you [ssh](https://en.wikipedia.org/wiki/Secure_Shell) into some random server halfway ’round the globe, Vim will be there.

This section includes only MVV (Minimum Viable Vim)—just enough to use Vim to do things like edit small configuration files or Git commits.[7](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-7) It’s not even really enough to be *dangerous*. If you’re interested in digging deeper, and especially if you’d like to use Vim as your primary editor, I recommend taking a look at [*Learn Enough Vim to Be Dangerous*](http://learnenough.com/vim-tutorial). But it’s worth noting that even mastering Minimum Viable Vim puts you in elite company—because Vim is so difficult, even a little Vim knowledge is the sort of thing can impress your friends (or a job interviewer).

### [1.1Starting Vim](https://www.learnenough.com/text-editor-tutorial#sec-starting_vim)

Unlike most of the modern editors discussed starting in [Section 2](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors), Vim can be run directly inside a terminal window, and requires no graphical interface.[8](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-8) All you do is type `vim` at the prompt:

```
$ vim

```

Typical results of running the `vim` command appear in [Listing 2](https://www.learnenough.com/text-editor-tutorial#code-vim_window) and [Figure 5](https://www.learnenough.com/text-editor-tutorial#fig-starting_vim). In both cases, the tildes (~) are not characters in the file but rather represent lines that have yet to be defined.

Listing 2: A textual representation of a Vim window (message and versions may differ).

```
~
~
~
~
~
~                              VIM - Vi IMproved
~
~                                 version 7.3
~                           by Bram Moolenaar et al.
~                 Vim is open source and freely distributable
~
~                        Help poor children in Uganda!
~                type  :help iccf<Enter>       for information
~
~                type  :q<Enter>               to exit
~                type  :help<Enter>  or  <F1>  for on-line help
~                type  :help version7<Enter>   for version info

```

![images/figures/starting_vim](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uowpiwuj30jg0f6dhq.jpg)

Figure 5: Vim running in a terminal window.

If starting Vim is easy, learning to use it, at least at first, can be incredibly hard. This is mostly due to Vim being a *modal* editor, which is probably unlike anything you have used before ([Box 4](https://www.learnenough.com/text-editor-tutorial#aside-modal_vim)). Vim has two principal *modes*, known as *normal mode* and *insertion mode*. Normal mode is for doing things like moving around the file, deleting content, or finding and replacing text, whereas insertion mode is for inserting text.

> Box 4. Modal Vim
>
> When I first started to learn programming in the Unix tradition (as opposed to my childhood experience with Microsoft DOS, BASIC, and Pascal), I distinctly recall being absolutely mortified at the unbelievably primitive editor I was expected to use. At the time, I was a first-year undergraduate at Harvard University, working in a [research group](https://www.cfa.harvard.edu/hea/sss/sun.html)at the [Harvard-Smithsonian Center for Astrophysics](https://www.cfa.harvard.edu/). The tool I had been handed was vi.To say that it seemed like a downgrade from word processors is a gross understatement ([Figure 1](https://www.learnenough.com/text-editor-tutorial#fig-y_u_no_word_processor)).
>
> What shocked me most about vi was modal editing: unlike word processors, vi didn’t let me just click in the window and start typing. Instead, there were a profusion of options (`i`, `a`, and `o` among them) for switching to *insertion mode*, and all it took was a few wrong keystrokes for all hell to break loose. Although the intervening years have seen a proliferation of more modern text editors, whose design is much more like the click-and-type interface I expected from my experience with word processors, the enduring popularity of vi (via Vim) means that learning the basics of modal editing is a valuable skill, even if it might at first seem ridiculously foreign.
>

Going back and forth between these two modes can cause a lot of confusion, especially since virtually all other programs that edit text (including word processors, email clients, and most text editors) have only insertion mode. Part of what makes Vim particularly confusing is that it *starts*in normal mode, which means that, if you try entering text immediately after starting Vim (as in [Listing 2](https://www.learnenough.com/text-editor-tutorial#code-vim_window)), the result will be chaos.

Because confusion is the likeliest result if you’re not used to Vim’s modal editing, we’re going to start our study of Vim with the *Most Important Vim Command™*. One of my college friends, who was a huge partisan of vi’s (and hence Vim’s) historical rival Emacs ([Box 5](https://www.learnenough.com/text-editor-tutorial#aside-holy_wars)), claimed the Most Important Vim Command™ was the only one he ever wanted to learn. Here it is:

```
ESC:q!

```

This command means “Press the Escape key, then type ‘colon q exclamation-point’.” We’ll learn in a moment what this does and why, but for now we’ll start by practicing it a couple of times in the exercises.

> Box 5. Holy wars: vi vs. Emacs
>
> The [Jargon File](http://www.catb.org/jargon/html/) defines [*holy wars*](http://www.catb.org/jargon/html/H/holy-wars.html) as follows:
>
> > **holy wars**: n.
> >
> > [from [*Usenet*](http://www.catb.org/jargon/html/U/Usenet.html), but may predate it; common][*flame war*](http://www.catb.org/jargon/html/F/flame-war.html)s over [*religious issues*](http://www.catb.org/jargon/html/R/religious-issues.html). The paper by Danny Cohen that popularized the terms [*big-endian*](http://www.catb.org/jargon/html/B/big-endian.html) and [*little-endian*](http://www.catb.org/jargon/html/L/little-endian.html) in connection with the LSB-first/MSB-first controversy was entitled *On Holy Wars and a Plea for Peace*.
> >
> > Great holy wars of the past have included [*ITS*](http://www.catb.org/jargon/html/I/ITS.html) vs. [*Unix*](http://www.catb.org/jargon/html/U/Unix.html), [*Unix*](http://www.catb.org/jargon/html/U/Unix.html) vs. [*VMS*](http://www.catb.org/jargon/html/V/VMS.html), [*BSD*](http://www.catb.org/jargon/html/B/BSD.html) Unix vs. System V, [*C*](http://www.catb.org/jargon/html/C/C.html) vs. [*Pascal*](http://www.catb.org/jargon/html/P/Pascal.html), [*C*](http://www.catb.org/jargon/html/C/C.html) vs. FORTRAN, etc. In the year 2003, popular favorites of the day are KDE vs. GNOME, vim vs. elvis, Linux vs. [Free|Net|Open]BSD. Hardy perennials include [*EMACS*](http://www.catb.org/jargon/html/E/EMACS.html) vs. [*vi*](http://www.catb.org/jargon/html/V/vi.html), my personal computer vs. everyone else’s personal computer, ad nauseam. The characteristic that distinguishes holy wars from normal technical disputes is that in a holy war most of the participants spend their time trying to pass off personal value choices and cultural attachments as objective technical evaluations. This happens precisely because in a true holy war, the actual substantive differences between the sides are relatively minor. See also [*theology*](http://www.catb.org/jargon/html/T/theology.html).
>
> As noted in the Jargon File entry, one of the longest-raging holy wars is fought between proponents of [vi](http://www.catb.org/jargon/html/V/vi.html) and its arch-rival [Emacs](http://www.catb.org/jargon/html/E/EMACS.html) (sometimes written “EMACS”), both of which have played important roles in the Unix computing tradition. Both also retain much popular support, although my guess is that, with the popularity of Vim, vi has taken a decisive lead in recent years. Of course, this is just the sort of statement that serves to perpetuate a holy war—likely prompting Emacs partisans to, say, make claims about the superior power and customizability of their favorite editor.
>
> If you wanted to start a *new* holy war, you might try something like, “Happily, the vi vs. Emacs holy war is now mostly a historical curiosity, as anyone who’s anyone has switched to a modern editor like Atom or Sublime.” It’s going to be quite a show—better bring some popcorn ([Figure 6](https://www.learnenough.com/text-editor-tutorial#fig-popcorn)).
>

![images/figures/popcorn](https://ws3.sinaimg.cn/large/006tNc79gy1fm6upndrs2g30cn09qu10.gif)

Figure 6: Watching a holy war play out ([Box 5](https://www.learnenough.com/text-editor-tutorial#aside-holy_wars)) can be entertaining.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_starting_vim)

1. Start Vim in a terminal, then run the Most Important Vim Command™.
2. Restart Vim in a terminal. Before typing anything else, type the string “This is a Vim document.” What happened? Confusing, right?
3. Use the Most Important Vim Command™ to recover from the previous exercise and return to the normal command-line prompt.

### [1.2Editing small files](https://www.learnenough.com/text-editor-tutorial#sec-editing_small_files)

Now that we know the Most Important Vim Command™ ([Section 1.1](https://www.learnenough.com/text-editor-tutorial#sec-starting_vim)), we’ll start learning how to use Vim for real by opening and editing a small file. In [Section 1.1](https://www.learnenough.com/text-editor-tutorial#sec-starting_vim), we started by running `vim` by itself, but it’s more common to use a filename as an argument. Let’s navigate to the home directory of our system and then open the file indicated:

```
$ cd
$ vim .bash_profile

```

This file, which probably already exists on your system (but will be created automatically by Vim if necessary), is used to configure the [*shell*](http://www.catb.org/jargon/html/S/shell.html), which is the program that supplies a command line.The default shell on most systems is *Bash*, a pseudo-acronym that stands for *Bourne Again SHell*.[9](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-9) As is common on Unix-based systems, the profile configuration file for Bash begins with a dot, indicating (as [noted](http://www.learnenough.com/command-line-tutorial#sec-listing) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial)) that the file is *hidden*, i.e., it doesn’t show up by default when listing directory contents with `ls` (or even when viewing the directory using a graphical file browser).

We’ll learn in [Section 1.3](https://www.learnenough.com/text-editor-tutorial#sec-saving_and_quitting_files) how to save changes to this file, but for now we’re just going to add some dummy content so that we can practice moving around. In [Section 1.1](https://www.learnenough.com/text-editor-tutorial#sec-starting_vim), we learned that Vim starts in normal mode, which means that we can change location, delete text, etc. Let’s go into insertion mode to add some content. The first step is to press the `i` key to *insert* text. Then, type a few lines (separated by returns), as shown in [Listing 3](https://www.learnenough.com/text-editor-tutorial#code-lorem_ipsum).[10](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-10) (There may be other existing content, which you should ignore for now.)

Listing 3: Adding some text after typing `i` to insert.`~/.bash_profile`

```
1 lorem ipsum
2 dolor sit amet
3 foo bar baz
4 I've made this longer than usual because I haven't had time to make it shorter.

```

After entering the text in [Listing 3](https://www.learnenough.com/text-editor-tutorial#code-lorem_ipsum), press `ESC` (the escape key) to switch from insertion mode back to normal mode.

Now that we have some text on a few lines, we can learn some commands for moving around small files. (We’ll cover some commands for navigating large files in [Section 1.5](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files).) The easiest way to move around is to use the arrow keys—up, down, left, right—which is what I recommend.[11](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-11) Vim has literally [jillions](https://www.youtube.com/watch?v=P64ikwUSs0A) of ways of moving around, and if you decide to use Vim as your primary text editor I recommend learning them, but for our purposes the arrow keys are fine. The only two additional commands I feel are essential are the ones to move to the beginning and end of the line, which are `0` and `$`, respectively.[12](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-12)

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_small_files)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Use the arrow keys to navigate to Line 4 in the file from [Listing 3](https://www.learnenough.com/text-editor-tutorial#code-lorem_ipsum).
2. Use the arrow keys to go to the end and then the beginning of Line 4. Cumbersome, eh?
3. Go to the beginning of Line 4 by using the command mentioned in the text.
4. Go to the end of Line 4 using the command mentioned in the text.

### [1.3Saving and quitting files](https://www.learnenough.com/text-editor-tutorial#sec-saving_and_quitting_files)

Having learned a little about moving around and inserting text, now we’re going to learn how to save a file. Our specific example will involve making a useful new Bash command, but first we have to deal with the current state of the Bash profile file. The text we added in [Listing 3](https://www.learnenough.com/text-editor-tutorial#code-lorem_ipsum) is gibberish (at least from Bash’s perspective), so what we’d like to do is quit the file without saving any changes. For [historical reasons](http://stackoverflow.com/questions/14051712/why-some-commands-in-vim-require-a-colon-while-some-dont), some Vim commands (especially those having to do with file manipulation) start with a colon `:`, and the normal way to quit a file is with `:q`, but that only works when there are no changes to save. In the present case, we get the error message “No write since last change (add ! to override)”, as shown in [Figure 7](https://www.learnenough.com/text-editor-tutorial#fig-no_quit).

![images/figures/no_quit](https://ws4.sinaimg.cn/large/006tNc79gy1fm6upwf4kig30cn09qu10.gif)

Figure 7: Trying to quit a file with unsaved changes.

Following the message’s advice, we can type `:q!` to force Vim to quit without saving any changes ([Figure 8](https://www.learnenough.com/text-editor-tutorial#fig-colon_q_bang)), which returns us to the command line.

![images/figures/colon_q_bang](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uq81psyg30cn09qu10.gif)

Figure 8: Forcing Vim to quit.

You may have noticed that we’re now in a position to understand the Most Important Vim Command™ introduced in [Section 1.1](https://www.learnenough.com/text-editor-tutorial#sec-starting_vim): no matter what terrible things you might have done to a file, as long as you type `ESC` (to get out of insertion mode if necessary)[13](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-13) followed by `:q!` (to force-quit) you are guaranteed not to do any damage.

Of course, Vim is only really useful if we can save our edits, so let’s add some useful text and then write out the result. As in [Section 1.2](https://www.learnenough.com/text-editor-tutorial#sec-editing_small_files), we’ll work on the `.bash_profile` file, and the edit we’ll make will add an *alias* to our shell. In a computing context, an alias is simply a synonym for a command or set of commands. The main use for Bash aliases is defining shorter commands for commonly used combinations. In this case, we’ll define the command `lr` (short for “list reverse”) as an alias for `ls -hartl`, which is the command to list files and directories using **h**uman-readable values for the sizes (e.g., 29K instead of 29592 for a 29-kilobyte file), including **a**ll of them (even hidden ones), ordered by **r**everse **t**ime, **l**ong form. This command, which as you may recognize from an [exercise](https://www.learnenough.com/command-line-tutorial#sec-exercises_downloading) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), is useful for seeing which files and directories have recently changed (as well as being, for obvious reasons, one of my personal favorites). After defining the alias, we’ll be able to replace the more verbose

```
$ ls -hartl

```

with the [pithier](http://dictionary.reference.com/browse/pithy)

```
$ lr

```

The steps appear as follows:

1. Press `i` to enter insertion mode.
2. Enter the contents shown in [Listing 4](https://www.learnenough.com/text-editor-tutorial#code-alias).
3. Press `ESC` to exit insertion mode.
4. Write the file using `:w`.
5. Quit Vim by typing `:q`.

*Note*: If you make any mistakes, you can type `ESC` followed by `u` to *undo* any of the previous steps. (Most programs use Command-Z or Ctrl-Z to undo things, yet another example of the non-native keybindings used by Vim. In contrast, the editors discussed starting in [Section 2](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors) all support native keybindings.)

Listing 4: Defining a Bash alias.`~/.bash_profile`

```
alias lr='ls -hartl'

```

After adding the `lr` alias to `.bash_profile`, writing the file, and quitting, you may be surprised to find that the command doesn’t yet work:

```
$ lr
-bash: lr: command not found

```

This is because we need to tell the shell about the updated Bash profile file by “sourcing” it using the `source` command, as shown in [Listing 5](https://www.learnenough.com/text-editor-tutorial#code-source_command).[14](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-14)

Listing 5: Activating the alias by sourcing the Bash profile.

```
$ source .bash_profile

```

With that, the `lr` command should work as advertised:

```
$ lr
.
.
.
drwx------+  15 mhartl  staff   510B Sep  4 18:58 Desktop
-rw-------    1 mhartl  staff    13K Sep  4 19:13 .viminfo
-rw-r--r--    1 mhartl  staff    46B Sep  4 19:14 .bash_profile
drwxr-xr-x+ 117 mhartl  staff   3.9K Sep  4 19:14 .

```

By the way, the `.bash_profile` file is sourced automatically when we open a new terminal tab or window, so explicit sourcing is necessary only when we want a change to be reflected in the *current* terminal.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_saving_and_quitting)

1. Define an alias `g` for the commonly used *case-insensitive grep* `grep -i`. What happens if, after making your changes and hitting `ESC`, you issue the command `:wq`instead of `:w` and `:q` separately?
2. You may [recall](https://www.learnenough.com/command-line-tutorial#sec-downloading_a_file) the `curl` command from [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), which lets us interact with URLs via the command line. Define `get` as an alias for `curl -OL`, which is the command to download a file to the local disk (while following any redirects encountered along the way).
3. Use the alias from the previous exercise to execute the command shown in [Listing 6](https://www.learnenough.com/text-editor-tutorial#code-sonnets), which downloads a longer text file for use in [Section 1.5](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files).

Listing 6: Downloading a longer text file for use in a future section.

```
$ get cdn.learnenough.com/sonnets.txt

```

### [1.4Deleting content](https://www.learnenough.com/text-editor-tutorial#sec-deleting_content)

As with every category of text manipulation, Vim has an enormous number of commands for deleting content, but in this section we’re just going to cover the absolute minimum. We’ll start with deleting single characters, which we can do in normal mode using the `x` command:

1. Open `.bash_profile` and insert the misspelled word `aliaes`
2. Get back to normal mode by pressing `ESC`
3. Move the cursor over the `e` in `aliaes` ([Figure 9](https://www.learnenough.com/text-editor-tutorial#fig-aliaes)) and press `x`

![images/figures/aliaes](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uqcat2sj30jg0f6gm4.jpg)

Figure 9: Preparing to delete a letter using `x`.

There are lots of fancy ways to delete text, but by repeatedly pressing `x` it’s easy (if a bit cumbersome) to delete entire words or even entire lines. On the other hand, deleting lines is enough of a special case to merit inclusion. Let’s get rid of the extra `alias` we added by pressing `dd` to delete the line. Voilà ! It should be gone ([Figure 10](https://www.learnenough.com/text-editor-tutorial#fig-no_alias)). To get it back, you can press `p` to “put” the line, which also allows you to simulate copying and pasting one line at a time. (Again, this is a minimal subset of Vim; if you decide to get good at it, you’ll learn lots of better ways to do things.)

![images/figures/no_alias](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uqdjbzej30jg0f63yz.jpg)

Figure 10: The result of deleting a line with `dd`.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises)

1. Using Vim, open a new file called `foo.txt`.
2. Insert the string “A leopard can’t change it’s spots.” ([Figure 11](https://www.learnenough.com/text-editor-tutorial#fig-leopard)).[15](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-15)
3. Using the `x` key, delete the character necessary to correct the mistake in the line you just entered. (If you can’t find the error, refer to [Table 1](https://www.learnenough.com/text-editor-tutorial#table-vim).)
4. Use `dd` to delete the line, then use `p` to paste it repeatedly into the document.
5. Save the document and quit using a single command. *Hint*: See the first exercise in [Section 1.3.1](https://www.learnenough.com/text-editor-tutorial#sec-exercises_saving_and_quitting).

![leopard](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uqigb5jj30jg0cx0zi.jpg)

Figure 11: This [animal](https://en.wikipedia.org/wiki/Leopard)’s spot-changing abilities are frequently questioned.

### [1.5Editing large files](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files)

The final skills needed for your Minimum Viable Vim involve navigating large files. If you didn’t download `sonnets.txt` in the exercises from [Section 1.3](https://www.learnenough.com/text-editor-tutorial#sec-saving_and_quitting_files), you should so do now ([Listing 7](https://www.learnenough.com/text-editor-tutorial#code-curl_sonnets)).[16](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-16)

Listing 7: Downloading Shakespeare’s *Sonnets*.

```
$ curl -OL cdn.learnenough.com/sonnets.txt

```

The resulting file contains the full text of Shakespeare’s *Sonnets*, which is 2620 lines, 17670 words, and 95635 characters long, which we can verify using the word count command `wc`[covered](https://www.learnenough.com/command-line-tutorial#sec-wordcount_and_pipes) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial):

```
$ wc sonnets.txt
    2620   17670   95635 sonnets.txt

```

On many systems, Vim shows some of the same basic stats upon opening the file:

```
$ vim sonnets.txt

```

The result on my system appears in [Figure 12](https://www.learnenough.com/text-editor-tutorial#fig-sonnets_stats). Because of its length, this file is far too long to navigate conveniently by hand.

![images/figures/sonnets_stats](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uqr611sj30jg0f6jvp.jpg)

Figure 12: Some file stats displayed upon starting Vim.

As before, there are lots of commands for moving around, but I find that the most useful ones involve moving a screen at a time, moving to the beginning or end, or searching. The commands to move one screen at a time are Ctrl-F (Forward) and Ctrl-B (Backward). To move to the end of the file, we can use `G`, and to move to the beginning we can use `1G`. Finally, perhaps the most powerful navigation command is *search*, which involves typing slash `/` followed by the string you want to find. The trick is to type `/<string>` followed by return, and then press `n` to go to the next match (if any).

This might all sound a little familiar, because it’s the same as the interface to the `less` program [covered](https://www.learnenough.com/command-line-tutorial#sec-less_is_more) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial).[17](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-17) This is one of the advantages of learning basic Unix commands: many of the patterns recur in many different contexts.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_editing_large)

1. With `sonnets.txt` open in Vim, move down three screens and then back up three screens.
2. Go to the end of the file. What is the last line of the final sonnet?
3. Navigate back to the top to change the old-style name “Shake-speare” on Line 1 of `sonnets.txt` to the more modern “Shakespeare”, and save the result.
4. Use Vim’s search feature to discover which sonnet contains references to Cupid, the Roman god of love.
5. Confirm that `18G` goes to the final line of the first sonnet. What do you suppose that command does? *Hint*: Recall that `1G` goes to the beginning of the file, i.e., Line 1.

### [1.6Summary](https://www.learnenough.com/text-editor-tutorial#sec-summary_vim)

Important commands from this section are summarized in [Table 1](https://www.learnenough.com/text-editor-tutorial#table-vim).

| **Command**  | **Description**                          |
| ------------ | ---------------------------------------- |
| `ESC:q!`     | The Most Important Vim Command™          |
| `i`          | Exit normal mode, enter insertion mode   |
| `ESC`        | Exit insertion mode, enter normal mode   |
| Arrow keys   | Move around                              |
| `0`          | Go to beginning of line                  |
| `$`          | Go to end of line                        |
| `:w`         | Save (write) a file                      |
| `:q`         | Quit a file (must be saved)              |
| `:wq`        | Write and quit a file                    |
| `:q!`        | Force-quit a file, discarding any changes |
| `u`          | Undo                                     |
| `x`          | Delete the character under the cursor    |
| `dd`         | Delete a line                            |
| `p`          | Put (paste) deleted text                 |
| `it’s spots` | No, you mean `its spots`                 |
| `Ctrl-F`     | Go forward one screen                    |
| `Ctrl-B`     | Go backward one screen                   |
| `G`          | Go to last line                          |
| `1G`         | Go to first line                         |
| `/<string>`  | Search for `<string>`                    |

Table 1: Important Vim commands from [Section 1](https://www.learnenough.com/text-editor-tutorial#sec-vim).

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_summary_vim)

1. Open `sonnets.txt`.
2. Go to the last line.
3. Go to the end of the last line.
4. Make a new line that says “That’s all, folks! Bard out. <drops mic>”. Make sure to move the cursor one space to the right so you don’t drag the final period along.
5. Write out the file.
6. Undo your changes.
7. Write out and quit the file.
8. Reopen the file and type `2620dd`.
9. Realize that you just deleted the entire file contents, and apply the Most Important Vim Command™ to ensure that no damage is done.

## [2Introduction to modern text editors](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors)

Having learned the minimal basics of text editing with Vim, we’re now in a good position to appreciate the preferred “modern” text editors mentioned at the beginning of this tutorial. These editors include cross-platform native editors such as [Sublime Text](http://www.sublimetext.com/) and [Atom](http://atom.io/), and editors in the cloud like [Nitrous](https://www.nitrous.io/) and [Cloud9](http://c9.io/). Modern editors are distinguished by their combination of power and ease-of-use: you can do fancy things like global search-and-replace, but (unlike Vim) they let you just click in a window and start typing. In addition, many of them (including Atom and Sublime) include an option to run in Vim compatibility mode, so even if you end up loving Vim you can still use a modern editor without having to give Vim up entirely.

Throughout the rest of this tutorial, we’ll explore the capabilities of modern text editors. We’ll end up covering all of the topics encountered in our discussion of Vim ([Section 1](https://www.learnenough.com/text-editor-tutorial#sec-vim)), as well as many more advanced subjects, including opening files, moving around, selecting text, cut/copy/paste, deleting and undoing, saving, and finding/replacing—all of which are important for day-to-day editing. We’ll also discuss both menu items and keyboard shortcuts, which help make your text editing faster and more efficient.

For future reference, [Table 2](https://www.learnenough.com/text-editor-tutorial#table-keyboard_symbols) shows the symbols for the various keys on a typical Macintosh keyboard. Apply your technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) if your keyboard differs.

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

Table 2: Miscellaneous keyboard symbols.

### [2.1Choosing a text editor](https://www.learnenough.com/text-editor-tutorial#sec-choosing_a_text_editor)

While cloud IDEs have many advantages, every aspiring computer magician should learn at least one native editor (i.e., an editor that runs on your desktop operating system). While there are many editors to choose from, probably the most promising modern text editors in use today are Atom and Sublime Text (sometimes just called “Sublime”).[18](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-18) Each has its own advantages and disadvantages.

#### [Atom](https://www.learnenough.com/text-editor-tutorial#sec-atom)

- Advantages
  1. Powerful, hackable, and easy to use
  2. Free both [as in speech and as in beer](https://en.wikipedia.org/wiki/Gratis_versus_libre) (i.e., it both costs nothing and is open-source software)
  3. Works cross-platform (Windows, macOS, Linux)
  4. Easy to set up command-line tools
  5. Backed by collaboration powerhouse [GitHub](http://github.com/)
- Disadvantages
  1. Slower than Sublime
  2. Based on browser technologies, which are largely untested in editors
  3. Not as mature as some alternatives

#### [Sublime Text](https://www.learnenough.com/text-editor-tutorial#sec-sublime_text)

- Advantages
  1. Powerful, hackable, and easy to use
  2. Can be used for free in “evaluation mode”
  3. Fast and robust, even when editing huge files/projects
  4. Works cross-platform (Windows, macOS, Linux)
  5. Backed by a profitable company that has a good track record of support and development
- Disadvantages
  1. Free in neither the speech nor beer senses
  2. Has a mildly annoying popup that goes away only if you buy a license
  3. Costs $70 as of this writing
  4. Setting up command-line tools takes some fiddling

It’s hard to go wrong with either of these choices, and my main day-to-day editor is currently Sublime Text, but because Atom is 100% free I think it’s probably the best choice for new users.The good news is that most of the skills in the sections that follow are universal, and if you learn Atom but decide to switch to Sublime Text (or even a cloud IDE) for your daily editing, most of the core ideas will translate easily.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_choosing)

Install and configure a text editor on your system as follows:

1. Download and install either [Atom](http://atom.io/) or [Sublime Text](http://www.sublimetext.com/). *Note*: Atom comes pre-installed on the Linux virtual machine described in [Box 2](https://www.learnenough.com/text-editor-tutorial#aside-virtual_machine), so if you’re using the VM you can skip this step.
2. If using Atom, go to Atom > Install shell commands to enable the `atom` command at the command line ([Figure 13](https://www.learnenough.com/text-editor-tutorial#fig-install_atom_shell_commands)).
3. If using Sublime Text, set up the `subl` command by Googling for “[sublime text command line](http://lmgtfy.com/?q=sublime+text+command+line)” and following the instructions for your system. Apply your technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) if you get stuck. You might also find it helpful to skip ahead to [Section 3.3](https://www.learnenough.com/text-editor-tutorial#sec-writing_an_executable_script) to learn about how to configure your system’s *path*.

![images/figures/install_atom_shell_commands](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uqziuxhj306o0bajs3.jpg)

Figure 13: Installing Atom’s shell commands.

### [2.2Opening](https://www.learnenough.com/text-editor-tutorial#sec-opening)

To open files, we’re going to use the command configured in [Section 2.1.3](https://www.learnenough.com/text-editor-tutorial#sec-exercises_choosing) to launch the editor and open the file at the same time (a method we used with `vim` in [Section 1.2](https://www.learnenough.com/text-editor-tutorial#sec-editing_small_files)). In [Section 3.4](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects), we’ll cover a second method (called “fuzzy opening”) that’s useful when editing a project with multiple files. I’ll assume you’re using the `atom` command, but if you’re using Sublime you should make the appropriate substitution (`subl` in place of `atom`).

Let’s get started by downloading a sample file, `README.md`, from the web. As in [Section 2.7.1](https://www.learnenough.com/text-editor-tutorial#sec-exercises_saving)and [Section 1.5](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files), we’ll use `curl` command to download the file at the command line:

```
$ curl -OL cdn.learnenough.com/README.md

```

As hinted at by the `.md` extension, the downloaded file is written in [Markdown](http://daringfireball.net/projects/markdown/), a human-readable markup language designed to be easy to convert to HTML, the language of the World Wide Web.

After downloading `README.md`, we can open it at the command line as follows:

```
$ atom README.md

```

(If this doesn’t work, be sure you’ve installed the Atom shell commands as shown in [Figure 13](https://www.learnenough.com/text-editor-tutorial#fig-install_atom_shell_commands).)The result of opening `README.md` in Atom should look something like [Figure 14](https://www.learnenough.com/text-editor-tutorial#fig-word_wrap_off) or [Figure 15](https://www.learnenough.com/text-editor-tutorial#fig-word_wrap_on). (If this is your first time opening Atom, it’s also possible you’ll see a one-time greeting screen. As usual, apply [Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication).) [Figure 14](https://www.learnenough.com/text-editor-tutorial#fig-word_wrap_off) shows the usual default, which is for “word wrap” to be off; because Markdown files are typically written using a long line for each paragraph, this setting isn’t ideal in this case, so I recommend turning on word wrap (called “soft wrap” in Atom) using the menu item shown in [Figure 16](https://www.learnenough.com/text-editor-tutorial#fig-toggle_soft_wrap).

![images/figures/word_wrap_off](https://ws2.sinaimg.cn/large/006tNc79gy1fm6ur41abpj30jg0kqq41.jpg)

Figure 14: The sample file with word wrap off.

![images/figures/word_wrap_on](https://ws2.sinaimg.cn/large/006tNc79gy1fm6ur5u796j30jg0kq411.jpg)

Figure 15: The sample file with word wrap on.

![images/figures/toggle_soft_wrap](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ur78h30j30820740ta.jpg)

Figure 16: The menu item to [toggle](https://en.wiktionary.org/wiki/toggle) word wrap.

In some editors, such as the cloud IDE at Cloud9, it’s more common to open files using the filesystem navigator (although in fact the `c9` command can be used to open files at the Cloud9 command line).[19](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-19) Double-clicking on `README.md` in the filesystem navigator ([Figure 17](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_filesystem_navigator)) opens the file in Cloud9’s editor, as shown in [Figure 18](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_post_doublclick). [Figure 19](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_word_wrap_off) shows the file after clicking “Navigate” to close the filesystem navigator, and we see that, as in [Figure 14](https://www.learnenough.com/text-editor-tutorial#fig-word_wrap_off), the line extends inconveniently off the screen. We can fix this using View > Wrap Lines as shown in [Figure 20](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_wrap_lines), with the word-wrapped result appearing as in [Figure 21](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_word_wrap_on). (Figuring out that a menu item like “View > Wrap Lines” turns on word wrap is exactly the kind of thing you should be able to figure out using your technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)).)

![images/figures/cloud9_filesystem_navigator](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ur96xdnj30jg0eoju1.jpg)

Figure 17: The Cloud9 filesystem navigator.

![images/figures/cloud9_post_doublclick](https://ws2.sinaimg.cn/large/006tNc79gy1fm6urb4t4rj30jg0eoju1.jpg)

Figure 18: Cloud9 after double-clicking on `README.md`.

![images/figures/cloud9_word_wrap_off](https://ws1.sinaimg.cn/large/006tNc79gy1fm6urd7gjmj30jg0eoabx.jpg)

Figure 19: Cloud9 with word wrap off.

![images/figures/cloud9_wrap_lines](https://ws2.sinaimg.cn/large/006tNc79gy1fm6urghh81j30jg0eowgj.jpg)

Figure 20: Turning word wrap on in Cloud9.

![images/figures/cloud9_word_wrap_on](https://ws1.sinaimg.cn/large/006tNc79gy1fm6urkl3k7j30jg0eo0w0.jpg)

Figure 21: Cloud9 with word wrap on.

#### [Syntax highlighting](https://www.learnenough.com/text-editor-tutorial#sec-syntax_highlighting)

One thing you may have noticed from inspecting [Figure 15](https://www.learnenough.com/text-editor-tutorial#fig-word_wrap_on) and [Figure 21](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_word_wrap_on) is that both Atom and Cloud9 display different aspects of the file in different colors. For example, Atom shows characters inside square brackets `[]` (which represent text for HTML links) in a lighter color than the rest of the text, while Cloud9 shows the same text in green. This is a practice known as *syntax highlighting*, which makes special text formatting much easier to identify visually. It’s essential to understand that this practice is strictly for our benefit; as far as the computer is concerned, the document in question is still plain text.

You might wonder how Atom and Cloud9 knew which highlighting scheme to use. The answer is that they infer the document format from the file type extension (in this case, `.md` for Markdown). The highlighting in Cloud9’s case is quite high-contrast, but in Atom’s case it isn’t particularly prominent; the most significant things are the different colors for the heading

```
# Sample document

```

and for links like

```
[Michael Hartl](http://michaelhartl.com/)

```

We’ll see more dramatic examples of syntax highlighting in [Section 2.7](https://www.learnenough.com/text-editor-tutorial#sec-saving) and especially in [Section 3.2](https://www.learnenough.com/text-editor-tutorial#sec-writing_source_code).

#### [Previewing Markdown](https://www.learnenough.com/text-editor-tutorial#sec-previewing_markdown)

As a final trick, I’d like to note that some editors, including Atom, can preview Markdown as HTML. We can figure out how to do this using our technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)), in this case by clicking on the Help menu and searching for “Preview” ([Figure 22](https://www.learnenough.com/text-editor-tutorial#fig-help)). The result is a built-in package called Markdown Preview, which converts Markdown to HTML and shows the result, as seen in [Figure 23](https://www.learnenough.com/text-editor-tutorial#fig-markdown_preview). In this context, it’s convenient to work with an expanded width so that both the source and the preview are wide enough to view easily, as seen in [Figure 24](https://www.learnenough.com/text-editor-tutorial#fig-wider_preview). This is accomplished by mousing over the side of the Atom window to get a double-arrow icon and then dragging to increase the size. We’ll see another example of this “double-paned” setup in a more general setting starting in [Section 3.4](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects).

![images/figures/help](https://ws4.sinaimg.cn/large/006tNc79gy1fm6urlzuf6j30ao05iaam.jpg)

Figure 22: Using the Help menu to learn how to preview Markdown.

![images/figures/markdown_preview](https://ws3.sinaimg.cn/large/006tNc79gy1fm6urqz74zj30jg0kpwj0.jpg)

Figure 23: A Markdown preview in Atom.

![images/figures/wider_preview](https://ws2.sinaimg.cn/large/006tNc79gy1fm6urt7tiaj30jg0bsq4v.jpg)

Figure 24: Using a wider window for the source and preview.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_opening)

1. By applying the methods in [Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication), find an online Markdown previewer (i.e., one that runs in a web browser), and use it to look at a preview of `README.md`. How do the results compare to [Figure 23](https://www.learnenough.com/text-editor-tutorial#fig-markdown_preview)?
2. Open a new document called `lorem.txt` and fill it with the text shown in [Listing 8](https://www.learnenough.com/text-editor-tutorial#code-lorem).Does the result have syntax highlighting?
3. Open a new document called `test.rb` and fill it with the text shown in [Listing 9](https://www.learnenough.com/text-editor-tutorial#code-test). Does the result have syntax highlighting?

Listing 8: Some lorem ipsum text.`~/lorem.txt`

```
Lorem ipsum dolor sit amet

```

Listing 9: A test file.`~/test.rb`

```
puts "test"

```

### [2.3Moving](https://www.learnenough.com/text-editor-tutorial#sec-moving)

Unlike the commands for moving around in Vim ([Section 1](https://www.learnenough.com/text-editor-tutorial#sec-vim), summarized in [Table 1](https://www.learnenough.com/text-editor-tutorial#table-vim)), the commands for moving around in modern editors generally match the techniques used in other programs such as word processors, email programs, and web browsers. As a result, it’s possible you may already know some or all of these techniques; if you don’t, by following the steps in this section you’ll get better at navigating other programs as a side-effect.

To get started, let’s open the large file from [Section 1.5](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files) consisting of the full text of Shakespeare’s *Sonnets*:

```
$ atom sonnets.txt

```

(If this doesn’t work, you may need to run the command in [Listing 7](https://www.learnenough.com/text-editor-tutorial#code-curl_sonnets), and you should also verify that you’re in the right directory.) The result appears in [Figure 25](https://www.learnenough.com/text-editor-tutorial#fig-atom_sonnets). Note that [Figure 25](https://www.learnenough.com/text-editor-tutorial#fig-atom_sonnets) shows `sonnets.txt` in its own tab, with `README.md` from [Section 2.2](https://www.learnenough.com/text-editor-tutorial#sec-opening) occupying the other tab. Your result may vary; in any case, we’ll discuss tabs further in [Section 3.4](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects).

![images/figures/atom_sonnets](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ury2iyaj30jg0kqtf8.jpg)

Figure 25: Opening Shakespeare’s *Sonnets* in Atom.

As with most other native programs such as word processors, web browsers, etc., you can move around a modern editor using the mouse or trackpad. You can click to place the cursor, scroll using a scroll wheel or [multi-touch gestures](https://support.apple.com/en-us/HT204895), or click and drag the scrollbar. The last of these is (as of this writing) incredibly subtle in Atom, so [Figure 26](https://www.learnenough.com/text-editor-tutorial#fig-scroll_bar) shows the scrollbar for Sublime Text.[Figure 26](https://www.learnenough.com/text-editor-tutorial#fig-scroll_bar) also shows the sort of two-pane view mentioned briefly in [Figure 24](https://www.learnenough.com/text-editor-tutorial#fig-wider_preview), which we’ll discuss more in [Section 3.4](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects).

![images/figures/scroll_bar](https://ws1.sinaimg.cn/large/006tNc79gy1fm6us6hq5fj30jg0bq7ac.jpg)

Figure 26: The Sublime Text scrollbar.

In addition to using the mouse or trackpad, I also like using the arrow keys to move around, typically in concert with the Command key ⌘ ([Table 2](https://www.learnenough.com/text-editor-tutorial#table-keyboard_symbols)). (In Linux, Command is typically replaced with the Function key fn, and in Windows it’s usually Ctrl, but you’ll have to apply [Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)to figure out the details.) My text editing typically involves lots of ⌘← and ⌘→ to move to the beginnings and ends of lines, and ⌘↑ and ⌘↓ to move to the top and bottom of the file. An example of moving to the end of the line in `README.md` appears in [Figure 27](https://www.learnenough.com/text-editor-tutorial#fig-move_end_of_line), and an example of moving to the end of the file in `sonnets.txt` appears in [Figure 28](https://www.learnenough.com/text-editor-tutorial#fig-move_end_of_file).

![images/figures/move_end_of_line](https://ws1.sinaimg.cn/large/006tNc79gy1fm6us9pnzyj30jg0kptb6.jpg)

Figure 27: Moving to the end of a line with ⌘→.

![images/figures/move_end_of_file](https://ws2.sinaimg.cn/large/006tNc79gy1fm6usfv41gj30jg0kqq9h.jpg)

Figure 28: Moving to the end of the file with ⌘↓.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_moving)

1. In your text editor, how do you move left and right one *word* at a time? *Hint:* On some systems, the Option key ⌥ might prove helpful.
2. In `README.md`, move to the second-to-last nonblank line using whatever technique you wish. Then move to the third word from the beginning of that line.
3. What is the command to go to a particular line *number*? Use this command to go to line 293 of `sonnets.txt`. What do rough winds do?
4. By moving to the last nonblank line of `sonnets.txt` and pressing ⌘→ followed by ⌘←, show that ⌘← actually stops as soon as it reaches [whitespace](https://en.wikipedia.org/wiki/Whitespace_character), with the result shown in [Figure 29](https://www.learnenough.com/text-editor-tutorial#fig-stop_on_whitespace). How do you get to the true beginning of the line?

![images/figures/stop_on_whitespace](https://ws3.sinaimg.cn/large/006tNc79gy1fm6usif5jdj30jg0jk456.jpg)

Figure 29: When using ⌘←, the cursor stops on whitespace.

### [2.4Selecting text](https://www.learnenough.com/text-editor-tutorial#sec-selecting_text)

Selecting text is an important skill that is particularly useful for deleting or replacing content, as well as for cutting, copying, and pasting ([Section 2.5](https://www.learnenough.com/text-editor-tutorial#sec-cut_copy_paste)). Many of the techniques in this section make direct application of the commands to move around covered in [Section 2.3](https://www.learnenough.com/text-editor-tutorial#sec-moving). As in that section, the ideas here are quite general, applying to a wide variety of applications, not just to text editors.

In much the same way that modern editors make it easy to use the mouse to move the cursor, they also make it easy to use the mouse to select text. Simply click and drag the mouse cursor, as shown in [Figure 30](https://www.learnenough.com/text-editor-tutorial#fig-mouse_drag_select). Another closely related technique is to click on one location, and then Shift-click on another location to select all the text in between.

![images/figures/mouse_drag_select](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uskxzhkj30jg0kq454.jpg)

Figure 30: The result of clicking and dragging the mouse cursor.

#### [Selecting a single word](https://www.learnenough.com/text-editor-tutorial#sec-selecting_a_single_word)

When selecting text, there are some special cases that are useful enough to consider individually.We’ll start with some techniques for selecting a single word:

- Click and drag the mouse cursor over the word
- Double-click the word with the mouse
- Press ⌘D (system-dependent; see [Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication))

#### [Selecting a single line](https://www.learnenough.com/text-editor-tutorial#sec-selecting_a_single_line)

Another technique, especially important when editing line-based text like computer code (or sonnets), involves selecting a full line or collection of lines. We start with ways to highlight a single line:

- Click the beginning of the line and drag the cursor to the end
- Click the end of the line and drag the cursor to the beginning
- Press ⌘← (twice) to get to the beginning of line, then press ⇧⌘→ to select to the end of line
- Press ⌘→ to get to the end of line, then press ⇧⌘← (twice) to select to the beginning of line

#### [Selecting multiple lines](https://www.learnenough.com/text-editor-tutorial#sec-selecting_multiple_lines)

A comparably important technique is selecting multiple lines:

- Click and drag the mouse cursor over the words/lines
- Hold down the Shift key and move the up and down arrow keys (⇧↑ and ⇧↓)

This latter technique is one of my personal favorites, and one of my most common editing tasks involves hitting ⌘← to go to the beginning of the first line I want to select and then hitting ⇧↓ repeatedly until I’ve selected all the lines I want ([Figure 31](https://www.learnenough.com/text-editor-tutorial#fig-down_arrow_multiple_lines)). (As noted in [Section 2.3.1](https://www.learnenough.com/text-editor-tutorial#sec-exercises_moving), in many editors ⌘← stops on whitespace, so moving to the beginning of the line actually requires two uses of ⌘← in succession. Being able to figure out details and [edge cases](https://en.wikipedia.org/wiki/Edge_case) like this is a hallmark of growing technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)).)

![images/figures/down_arrow_multiple_lines](https://ws3.sinaimg.cn/large/006tNc79gy1fm6usoch5jj30jg0kqn3t.jpg)

Figure 31: Selecting a Shakespearean couplet using ⌘← and ⇧↓.

#### [Selecting the entire document](https://www.learnenough.com/text-editor-tutorial#sec-selecting_the_entire_document)

Finally, it’s sometimes useful to be able to select the entire document at once. For this, there are two main techniques:

- Use a menu item called “Select All” or something similar. The specifics are editor-dependent; [Figure 32](https://www.learnenough.com/text-editor-tutorial#fig-selection_menu_select_all) shows the use of the Selection menu in Sublime Text, while [Figure 33](https://www.learnenough.com/text-editor-tutorial#fig-edit_menu_select_all)shows the use of the Edit menu in Atom.
- Press ⌘A

Note from [Figure 32](https://www.learnenough.com/text-editor-tutorial#fig-selection_menu_select_all) that the menu actually shows the corresponding command (⌘A); bootstrapping your knowledge using the menu items is a great way to learn keyboard shortcuts, which over time will make your text editing significantly more efficient.

![images/figures/selection_menu_select_all](https://ws3.sinaimg.cn/large/006tNc79gy1fm6usq9z89j309d07ugma.jpg)

Figure 32: Selecting the entire document using the Selection menu (Sublime Text).

![images/figures/edit_menu_select_all](https://ws2.sinaimg.cn/large/006tNc79gy1fm6usrnbd1j30730bodgp.jpg)

Figure 33: Selecting the entire document using the Edit menu (Atom).

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_selecting)

1. Select Shakespeare’s second sonnet by clicking at the beginning and then Shift-clicking at the end.
2. Select the first line in the file by moving to the beginning with ⌘↑ and pressing ⇧⌘→ (or the equivalent for your system).
3. Delete the selection in the previous exercise (using the Delete key).
4. Select the word “document” in `README.md` and replace it with “README”.

### [2.5Cut, copy, paste](https://www.learnenough.com/text-editor-tutorial#sec-cut_copy_paste)

The Cut/Copy/Paste [triumvirate](http://dictionary.reference.com/browse/triumvirate) is one of the most useful sets of operations when editing text, especially when executed via the conveniently located keyboard shortcuts ⌘X/⌘C/⌘V.(Cut/Copy/Paste are available as menu items ([Figure 34](https://www.learnenough.com/text-editor-tutorial#fig-ccp_menu)), but the operations are so common that I strongly recommend learning and using the keyboard shortcuts right away.) Although only ⌘C is [mnemonic](http://dictionary.reference.com/browse/mnemonic?s=t) (“C” for “Copy”), the keys are conveniently located three in a row on the bottom row of a standard QWERTY keyboard, which makes it easy to use them in combination or in quick succession ([Figure 35](https://www.learnenough.com/text-editor-tutorial#fig-keyboard_xcv)).

![images/figures/ccp_menu](https://ws2.sinaimg.cn/large/006tNc79gy1fm6ustl2etj306z0boq3s.jpg)

Figure 34: The Cut/Copy/Paste menu items (which you should never use).

![images/figures/keyboard_xcv](https://ws4.sinaimg.cn/large/006tNc79gy1fm6usvo1osj30jg09fjus.jpg)

Figure 35: The XCV keys on a standard QWERTY keyboard.

Applying either Cut or Copy involves first selecting text ([Section 2.4](https://www.learnenough.com/text-editor-tutorial#sec-selecting_text)), and then hitting either ⌘X to Cut or ⌘C to Copy. When using ⌘C to Copy, the selected text is placed in a *buffer* (temporary memory area); moving to the desired location ([Section 2.3](https://www.learnenough.com/text-editor-tutorial#sec-moving)) and hitting ⌘V lets you Paste the content into the document at the location of the cursor. ⌘X works the same way as ⌘C, except the text is removed from the document as well as being copied into the buffer.

As a concrete example, let’s select a Markdown link from the sample `README` file, `README.md`, as shown in [Figure 36](https://www.learnenough.com/text-editor-tutorial#fig-select_link). After copying with ⌘C, we can then paste the link several times (with returns in between) by repeatedly hitting ⌘V and the Enter key, as shown in [Figure 37](https://www.learnenough.com/text-editor-tutorial#fig-pasting_link). Finally, [Figure 38](https://www.learnenough.com/text-editor-tutorial#fig-cut_and_paste) shows the result of cutting `README` from the main text and pasting it in at the end of the file.

![images/figures/select_link](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ut097boj30jg0kp0v6.jpg)

Figure 36: Selecting a Markdown link

![images/figures/pasting_link](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ut3ife0j30jg0kp779.jpg)

Figure 37: Pasting link text several times (with returns in between).

![images/figures/cut_and_paste](https://ws4.sinaimg.cn/large/006tNc79gy1fm6ut7ifk5j30jg0kqjuf.jpg)

Figure 38: The result of cutting “README” and pasting at the end of the file.

#### [Jumpcut](https://www.learnenough.com/text-editor-tutorial#sec-jumpcut)

Although Cut/Copy/Paste is all that’s strictly necessary for everyday editing, there is one big downside, which is that there is only room in the buffer for a single string. Among other things, this means that if you Cut something and then accidentally hit “copy” instead of “paste” (which is easy since the letters are adjacent on the keyboard), you overwrite the buffer, and the text you Cut is gone forever (unless you undo as described in [Section 2.6](https://www.learnenough.com/text-editor-tutorial#sec-deleting_and_undoing)). If you happen to be developing on a Mac, there’s a solution to this problem: a free program called [Jumpcut](http://jumpcut.sourceforge.net/). This remarkable little utility app expands the buffer by maintaining more than one entry in the history. You can navigate this expanded buffer either using the Jumpcut menu ([Figure 39](https://www.learnenough.com/text-editor-tutorial#fig-jumpcut)) or the keyboard shortcuts ⌃⌥V (cycle forward) and ⇧⌃⌥V (cycle backward). I use Jumpcut dozens or even hundreds of times a day, and I strongly suggest giving it a try.

![images/figures/jumpcut](https://ws1.sinaimg.cn/large/006tNc79gy1fm6utf384aj309l09rq3o.jpg)

Figure 39: Jumpcut expands the copy-and-paste buffer to include a longer history.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_cut_copy_paste)

1. Select the entire document, Copy it, and Paste several times. The result should look something like [Figure 40](https://www.learnenough.com/text-editor-tutorial#fig-many_pastes).
2. Select the entire document and Cut it. Why might this be preferable to deleting it?
3. Select and copy the couplet at the end of Sonnet 1 and paste it into a new file called `sonnet_1.txt`. How do you create a new file directly in your editor?

![images/figures/many_pastes](https://ws3.sinaimg.cn/large/006tNc79gy1fm6utivrk1j30jg0kq7bf.jpg)

Figure 40: The result of pasting the whole document several times.

### [2.6Deleting and undoing](https://www.learnenough.com/text-editor-tutorial#sec-deleting_and_undoing)

We mentioned deleting before in [Section 2.4.5](https://www.learnenough.com/text-editor-tutorial#sec-exercises_selecting) (the exercises for [Section 2.4](https://www.learnenough.com/text-editor-tutorial#sec-selecting_text)), which of course simply involves pressing the Delete key, sometimes written as ⌫ ([Table 2](https://www.learnenough.com/text-editor-tutorial#table-keyboard_symbols)). As with Cut/Copy/Paste ([Section 2.5](https://www.learnenough.com/text-editor-tutorial#sec-cut_copy_paste)), deletion is especially useful when combined with the selection techniques from [Section 2.4](https://www.learnenough.com/text-editor-tutorial#sec-selecting_text).

In addition to the obvious technique of selecting and deleting text, on a Mac I especially like using ⌥⌫ to delete one word at a time. I’ll frequently use this combination if I need to delete a medium number of words (say 2–5) to restart a phrase when writing. For shorter deletion tasks, such as one word, it’s usually faster to hit ⌫ repeatedly, as context-switching to use ⌥⌫ incurs some overhead that makes it faster to just delete directly. Don’t worry too much about these micro-optimizations, though; with experience, as a matter of course you’ll come up with your own set of favorite techniques.

Paired with deletion is one of the most important commands in the history of the Universe, Undo. In modern editors, Undo uses the native keybinding, typically ⌘Z or ⌃Z. Its inverse, Redo, is usually something like ⇧⌘Z or ⌘Y. You can also use the menu (typically Edit), but, as with Cut/Copy/Paste ([Section 2.5](https://www.learnenough.com/text-editor-tutorial#sec-cut_copy_paste)), Undo is so useful that I recommend memorizing the shortcut as soon as possible. Without Undo, operations like deletion would be irreversible and hence potentially harmful, but with Undo it’s easy to reverse any mistakes you make while editing.

![images/figures/undo_redo](https://ws1.sinaimg.cn/large/006tNc79gy1fm6utks1xhj306z0bo3zc.jpg)

Figure 41: Undo and Redo in the editor menu.

One practice I recommend is using Cut instead of Delete whenever you’re not 100% sure you’ll never want the content again. Although you can usually Undo your way to safety if you accidentally delete something important, putting the content into the buffer with Cut gives you an additional layer of redundancy. (Using Jumpcut ([Section 2.5.1](https://www.learnenough.com/text-editor-tutorial#sec-jumpcut)) gives you another layer still.)

Finally, Undo provides us with a useful trick for finding the cursor, a common task when editing larger files. The issue is that you’ll be writing some text and then need to move ([Section 2.3](https://www.learnenough.com/text-editor-tutorial#sec-moving)) or find ([Section 2.8](https://www.learnenough.com/text-editor-tutorial#sec-finding_and_replacing)) elsewhere in the document. On these occasions, it can be hard to relocate the cursor. There are several ways around this problem—you can move the arrow keys, or just start typing—but my favorite technique is to Undo and then immediately Redo (⌘Z/⇧⌘Z or ⌘Z/⌘Y), which is guaranteed to find the cursor without making any undesired changes.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_deleting)

1. Use Undo repeatedly until all the changes you’ve made to `README.md` have been undone.
2. Using any technique you want from [Section 2.4](https://www.learnenough.com/text-editor-tutorial#sec-selecting_text), select the word “written” in `README.md`and delete it, then undo the change.
3. Redo the change from the previous exercise, then undo it again.
4. Make an edit somewhere in `sonnets.txt`, then scroll around so you get lost. Use the Undo/Redo trick to find the cursor again. Then keep using Undo to undo all your changes.

### [2.7Saving](https://www.learnenough.com/text-editor-tutorial#sec-saving)

Once we’ve made some edits to a file, we can save it using the menu or with ⌘S. I strongly recommend using the keyboard shortcut, which among other things makes it easier to save the file whenever you reach a temporary pause in your writing or coding—a valuable habit to cultivate. Basically, if you’re not doing something else, you should be hitting Save. This habit goes a long way toward preventing lost work (and, as discussed in [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial), is especially powerful when combined with version control).

As an example, we can add some source code to our README file and save the result. We start by pasting in the code from [Listing 10](https://www.learnenough.com/text-editor-tutorial#code-code_snippet), as shown in [Figure 42](https://www.learnenough.com/text-editor-tutorial#fig-unsaved_file) (which includes some nice high-contrast syntax highlighting). As you can see from the circled indicator in [Figure 42](https://www.learnenough.com/text-editor-tutorial#fig-unsaved_file), Atom (as with most modern editors) includes a subtle indicator that the file is unsaved, in this case a small open circle. After running Save (via ⌘S, for example), the circle disappears, to be replaced with an X ([Figure 43](https://www.learnenough.com/text-editor-tutorial#fig-saved_file)).

Listing 10: A code snippet.

```
​```ruby
def hello
  puts "hello, world!"
end
​```

```

![images/figures/unsaved_file](https://ws1.sinaimg.cn/large/006tNc79gy1fm6utubn1vj30jg0kpmzt.jpg)

Figure 42: An unsaved file.

![images/figures/saved_file](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uu4omhoj30jg0kpmzt.jpg)

Figure 43: The file from [Figure 42](https://www.learnenough.com/text-editor-tutorial#fig-unsaved_file) after saving.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_saving)

1. Undo the pasting in of source code to restore the file to its original state.
2. Figure out how to “Save As”, then save `README.md` as `code_example.md`, paste in the code example, and save the file.
3. The default Bash prompt for my command-line terminal appears as in [Listing 11](https://www.learnenough.com/text-editor-tutorial#code-default_prompt), but I prefer the more compact prompt shown in [Listing 12](https://www.learnenough.com/text-editor-tutorial#code-custom_prompt). In [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), I [promised](https://www.learnenough.com/command-line-tutorial#sec-navigating_directories) to show how to customize the prompt in *Learn Enough Text Editor to Be Dangerous*. Fulfill this promise by editing the `.bash_profile` file to include the lines shown in [Listing 13](https://www.learnenough.com/text-editor-tutorial#code-customize_prompt). Source the Bash profile as in [Listing 5](https://www.learnenough.com/text-editor-tutorial#code-source_command) and confirm that the prompt on your system matches the one shown in [Listing 12](https://www.learnenough.com/text-editor-tutorial#code-custom_prompt).

Listing 11: The default terminal prompt on my system.

```
MacBook-Air:~ mhartl$

```

Listing 12: My preferred, more compact prompt.

```
[~]$

```

Listing 13: The Bash lines needed to customize the prompt as shown in [Listing 12](https://www.learnenough.com/text-editor-tutorial#code-custom_prompt).`~/.bash_profile`

```
alias lr='ls -hartl'
# Customize prompt to show only working directory.
PS1='[\W]\$ '

```

### [2.8Finding and replacing](https://www.learnenough.com/text-editor-tutorial#sec-finding_and_replacing)

One of the most powerful features of every good text editor is the ability to *find* and optionally *replace* text. In this section we’ll learn how to find and replace in a single file; in [Section 3.4](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects) we’ll discuss the more powerful (and *much* more dangerous) method of finding and replacing across multiple files.

To find inside a file, you can use the Find menu, shown in [Figure 44](https://www.learnenough.com/text-editor-tutorial#fig-find_menu), which also shows that ⌘F is the corresponding keyboard shortcut. Either one brings up a [*modal window*](https://en.wikipedia.org/wiki/Modal_window) where you can type in the string you’re searching for ([Figure 45](https://www.learnenough.com/text-editor-tutorial#fig-modal_window)).

![images/figures/find_menu](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uu7gvu0j306p09kmxt.jpg)

Figure 44: Finding using the menu.

![images/figures/modal_window](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uug2sn8j30j8038dg3.jpg)

Figure 45: A modal window for finding and replacing.

For example, suppose we search for the string “sample”. As seen in [Figure 46](https://www.learnenough.com/text-editor-tutorial#fig-find_sample), both “Sample” and “sample” are highlighted. The reason our search finds both is because we’ve opted to search case-insensitively (which is usually the default).

![images/figures/find_sample](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uuti6pmj30jg0kpadu.jpg)

Figure 46: Finding the string “sample”.

[Figure 47](https://www.learnenough.com/text-editor-tutorial#fig-find_replace) shows how to use the modal window to find “sample” and replace with “example”. In order to avoid replacing “Sample”, we first click on Find to select the next match, and then click on Replace to replace the second match ([Figure 48](https://www.learnenough.com/text-editor-tutorial#fig-replaced)). (Changing to case-sensitive search would also work in this case; learning how to do this is left as an exercise ([Section 2.8.1](https://www.learnenough.com/text-editor-tutorial#sec-exercises_find_replace)).)

![images/figures/find_replace](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uviuwgnj30jg0kp0vw.jpg)

Figure 47: Finding and replacing.

![images/figures/replaced](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uvpmpf3j30jg0kpjui.jpg)

Figure 48: The result of replacing “sample” with “example”.

As seen in [Figure 44](https://www.learnenough.com/text-editor-tutorial#fig-find_menu), you can also type ⌘G to find the next match using a keyboard shortcut.This ⌘F/⌘G combination also works in many other applications, such as word processors and web browsers.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_find_replace)

1. In [Section 2.3.1](https://www.learnenough.com/text-editor-tutorial#sec-exercises_moving), we found Sonnet 18 by going directly to line 293, but of course I didn’t search the file line by line to write the exercise. Instead, I searched for “shall I compare thee”. Use your text editor to search for this string in `sonnets.txt`. On what line does “rosy lips and cheeks” appear?
2. The example in this section shows one of the pitfalls of mechanically finding and replacing text: we’ve ended up with the ungrammatical result “a example” instead of “an example”. Rather than fix this by hand, use find and replace to replace “a example” with “an example” in your document. (Although in the present case there’s only one occurrence, this more general technique scales up to documents much longer than our toy example.)
3. What is the keyboard shortcut in your editor for finding the previous match?
4. What is the keyboard shortcut to replace in the current buffer (file)? How does this differ from the keyboard shortcut for simply finding?

### [2.9Summary](https://www.learnenough.com/text-editor-tutorial#sec-summary_modern_text_editors)

- Atom and Sublime Text are both excellent choices for a primary modern text editor.
- One common way to open files is to use a command at the command line.
- For files containing things like prose with long lines, it’s a good idea to turn on word wrap.
- Moving around text files can be accomplished many different ways, including using the mouse and arrow keys (especially in combination with the Command/Control key).
- One convenient way to select text is to hold down Shift and move the cursor.
- The Cut/Copy/Paste triumvirate is incredibly useful.
- Undo can save your bacon ([Figure 49](https://www.learnenough.com/text-editor-tutorial#fig-bacon)).[20](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-20)

![images/figures/bacon](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uvsl3cmj30jg0d0jws.jpg)

Figure 49: Undo can save your bacon.

Important commands from this section are summarized in [Table 3](https://www.learnenough.com/text-editor-tutorial#table-modern_text_editors).

| **Command** | **Description**                          |
| ----------- | ---------------------------------------- |
| ⌘←          | Move to beginning of line (stops on whitespace) |
| ⌘→          | Move to end of line                      |
| ⌘↑          | Move to beginning of file                |
| ⌘↓          | Move to end of file                      |
| ⇧-move      | Select text                              |
| ⌘D          | Select current word                      |
| ⌘A          | Select All (entire document)             |
| ⌘X/⌘C/⌘V    | Cut/Copy/Paste                           |
| ⌘Z          | Undo                                     |
| ⇧⌘Z or ⌘Y   | Redo                                     |
| ⌘S          | Save                                     |
| ⌘F          | Find                                     |
| ⌘G          | Find next                                |

Table 3: Important commands from [Section 2](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors).

## [3Advanced text editing](https://www.learnenough.com/text-editor-tutorial#sec-advanced_text_editing)

Having covered the basic functions of modern text editors in [Section 2](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors), in this section we’ll learn about a few of the most common advanced topics. Even more than in [Section 2](https://www.learnenough.com/text-editor-tutorial#sec-modern_text_editors), details will vary based on the exact editor you choose, so use your growing technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) to figure out any necessary details. The most important lesson is that the advanced functions in this section are all things that *any* professional-grade editor can do, so you should be able to figure out how to do them no matter which editor you’re using.

### [3.1Autocomplete and tab triggers](https://www.learnenough.com/text-editor-tutorial#sec-autocomplete_tab_triggers)

Two of the most useful features of text editors are *autocomplete* and *tab triggers*, which you can think of as roughly command-line style tab completion for text files. (See [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial) for details on [tab completion](https://www.learnenough.com/command-line-tutorial#aside-tab_completion).) Both features allow us to type potentially large amounts of text with only a few keystrokes.

#### [Autocomplete](https://www.learnenough.com/text-editor-tutorial#sec-autocomplete)

The most common variant of autocomplete lets us type the first few letters of a word and then gives us the ability to complete it from a menu of options, typically by using the arrow keys and hitting Tab to accept the completion. An example of autocompleting the word “Markdown” in `README.md` appears in [Figure 50](https://www.learnenough.com/text-editor-tutorial#fig-autocomplete).

![images/figures/autocomplete](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uvwk3c2j30jg0kqju3.jpg)

Figure 50: Autocomplete for “Markdown”.

The autocomplete menu itself is populated using the current document, so autocomplete is particularly useful in longer documents that contain a large number of possible completions. For instance, the source for *Learn Enough Text Editor to Be Dangerous* (which is written using the powerful markup language LATEX) makes use of a large number of labels for making cross-references, and these labels are often long enough that it’s much easier to autocomplete them than to type them out by hand. An example is the oft-cited [Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication), whose source looks like [Listing 14](https://www.learnenough.com/text-editor-tutorial#code-autocomplete).

Listing 14: A cross-reference with a label I usually autocomplete.

```
Box~\ref{aside:technical_sophistication}

```

When writing the string `technical_sophistication` in [Listing 14](https://www.learnenough.com/text-editor-tutorial#code-autocomplete), I nearly always use autocomplete instead of typing it out in full.[21](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-21) (As mentioned below, the rest of the cross-reference is generated using a custom tab trigger.) Similar considerations frequently occur when writing source code, where (as we’ll learn in [*Learn Enough Ruby to Be Dangerous*](http://learnenough.com/ruby-tutorial)) we might encounter something like this:

```
ReallyLongClassName < ReallyLongBaseClassName

```

In such cases, rather than typing out the long names by hand, it’s usually easier to type `Rea` and then select the relevant autocompletion.

#### [Tab triggers](https://www.learnenough.com/text-editor-tutorial#sec-tab_triggers)

Tab triggers are similar to autocompletion in that they let us type a few letters and then hit *tab* to work some magic, but in this case many of them come pre-defined with the editor, with the exact triggers typically based on the particular type of document we’re editing. For example, in Markdown and other markup files (HTML, LATEX, etc.), typing `lorem⇥` or `lo⇥` yields so-called *lorem ipusum* text, a Latin fragment from [Cicero](https://en.wikipedia.org/wiki/Cicero) that is [often used as dummy text](http://www.straightdope.com/columns/read/2290/what-does-the-filler-text-lorem-ipsum-mean) in programming and design. We saw *lorem ipsum* briefly before in [Listing 8](https://www.learnenough.com/text-editor-tutorial#code-lorem); a second example appears in [Figure 51](https://www.learnenough.com/text-editor-tutorial#fig-tab_trigger), which shows the result of typing `lo` in Atom. A closeup appears in [Figure 52](https://www.learnenough.com/text-editor-tutorial#fig-tab_trigger_detail). After hitting ⇥ to invoke the tab trigger, the full *lorem ipsum* text appears as in [Figure 53](https://www.learnenough.com/text-editor-tutorial#fig-tab_trigger_result).

![images/figures/tab_trigger](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uw3pbfuj30jg0kqgoa.jpg)

Figure 51: Typing “lo” in Atom prepares to activate a tab trigger.

![images/figures/tab_trigger_detail](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uw5e77kj306b020aa2.jpg)

Figure 52: A more detailed view of the trigger in [Figure 51](https://www.learnenough.com/text-editor-tutorial#fig-tab_trigger).

![images/figures/tab_trigger_result](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uw868ezj30jg0kq78v.jpg)

Figure 53: The result of the tab trigger in [Figure 51](https://www.learnenough.com/text-editor-tutorial#fig-tab_trigger).

Tab triggers are especially useful when editing source code. For instance, when writing Ruby code, typing `def⇥` in Atom creates a Ruby *define* statement to make a *function*, which looks like this:

```
def method_name

end

```

After typing the name of the function (which replaces the placeholder text `method_name`), we can hit ⇥ again to place the cursor in the right location to start writing the main part of the function. These sorts of auto-expansions of content can speed up code production considerably, while also lowering the [cognitive load](https://en.wikipedia.org/wiki/Cognitive_load) of programming. We’ll learn more about using tab triggers in [*Learn Enough Ruby to Be Dangerous*](http://learnenough.com/ruby-tutorial).

Finally, it’s possible to define tab triggers of your own. My own editing makes extensive use of tab triggers; for example, to make the text in [Listing 14](https://www.learnenough.com/text-editor-tutorial#code-autocomplete), instead of typing

```
Box~\ref{aside:foo}

```

by hand I used the custom tab trigger `bref` (for “box reference”). (Of course, I then completed the part of the label after `aside:` using autocomplete.) Custom tab triggers are beyond the scope of this tutorial, but some hints about how to figure it out for yourself appear in [Section 3.5](https://www.learnenough.com/text-editor-tutorial#sec-customization).

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_tab_triggers)

1. Add some more *lorem ipsum* text to `README.md` using a tab trigger.
2. Add another occurrence of the word “consectetur” using autocomplete.
3. Write the sentence “As Cicero once said, ‘quis nostrud exercitation ullamco laboris’.” with the help of as many uses of autocomplete as you want.

### [3.2Writing source code](https://www.learnenough.com/text-editor-tutorial#sec-writing_source_code)

In addition to being good at editing markup like HTML and Markdown, text editors excel at writing computer programs. Any good programmer’s text editor supports many specialized functions for writing code; this section covers a few of the most useful. Even if you don’t know how to program (yet!), it’s still useful to know about some of the ways text editors support writing code.

An example of computer code appears in [Listing 15](https://www.learnenough.com/text-editor-tutorial#code-ruby_hello), which shows a variant of a “[hello, world](http://www.catb.org/jargon/html/H/hello-world.html)” program written in the Ruby programming language. (You are not expected to understand this program.)

Listing 15: A variant of “hello, world” in Ruby.

```
1 # Prints a greeting.
2 def hello(location)
3   puts "hello, #{location}!"
4 end
5
6 hello("world")

```

To see the contents from [Listing 15](https://www.learnenough.com/text-editor-tutorial#code-ruby_hello) in a text editor, we can fire up Atom as follows:

```
$ atom hello.rb

```

Upon pasting in the content of [Listing 15](https://www.learnenough.com/text-editor-tutorial#code-ruby_hello), we get the result shown in [Figure 54](https://www.learnenough.com/text-editor-tutorial#fig-ruby_hello). (For extra credit, type in [Listing 15](https://www.learnenough.com/text-editor-tutorial#code-ruby_hello) by hand using the `def` tab trigger discussed in [Section 3.1](https://www.learnenough.com/text-editor-tutorial#sec-autocomplete_tab_triggers).)

![images/figures/ruby_hello](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uw9xmz7j30jg0kq3zi.jpg)

Figure 54: A Ruby program in Atom.

#### [Syntax highlighting](https://www.learnenough.com/text-editor-tutorial#sec-modern_syntax_highlighting)

As we saw in [Section 2.2.1](https://www.learnenough.com/text-editor-tutorial#sec-syntax_highlighting) with `README.md`, Atom uses the filename extension to determine the proper syntax highlighting. In that case the (rather subtle) highlighting was for Markdown; in this case, Atom infers from `.rb` that the file contains Ruby code, and highlights it accordingly.As before, it’s essential to understand that the highlighting isn’t inherent to the text, which is still plain. Syntax highlighting is purely for our benefit as readers of the code.

In addition to making it easier to parse the source code visually (i.e., distinguishing keywords, strings, constants, etc.), syntax highlighting can also be useful for catching bugs. For example, at one point when editing [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial) I accidentally deleted a LATEX closing quote (which consists of the two single quotes `''`), with the result shown in [Figure 55](https://www.learnenough.com/text-editor-tutorial#fig-syntax_highlight_debugging_before). This changed the color of the main text from the default white to the color used for quoted strings (green), which made it apparent at a glance that something was wrong. Upon fixing the error, the highlighting changed back to the expected white text, as shown in [Figure 56](https://www.learnenough.com/text-editor-tutorial#fig-syntax_highlight_debugging_after).

![images/figures/syntax_highlight_debugging_before](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uwchtq6j30fs04sab0.jpg)

Figure 55: An error in LATEX source caught by syntax highlighting.

![images/figures/syntax_highlight_debugging_after](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uwffc2mj30fx04oq3w.jpg)

Figure 56: Error fixed, syntax highlighting as expected.

#### [Commenting out](https://www.learnenough.com/text-editor-tutorial#sec-commenting_out)

One of the most useful functions of a text editor is the ability to “comment out” blocks of code, a technique often used to temporarily prevent execution of certain lines without having to delete them entirely (which is often particularly helpful when debugging). Most programming and markup languages support comment lines that exist for the benefit of humans reading the code but are ignored by the programming language itself.[22](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-22) An example of a Ruby comment appears in the first line of [Listing 15](https://www.learnenough.com/text-editor-tutorial#code-ruby_hello):

```
# Prints a greeting.

```

Here the leading hash symbol `#` is Ruby’s way of indicating a comment line.

Suppose we wanted to comment out the next three lines (lines 2–4), to change

```
# Prints a greeting.
def hello(location)
  puts "hello, #{location}!"
end

hello("world")

```

to

```
# Prints a greeting.
# def hello(location)
#  puts "hello, #{location}!"
# end

hello("world")

```

It’s possible to do this by hand, of course, simply by inserting a `#` at the beginning of each line.This is inconvenient, though, and becomes increasingly so as the length of the commented-out text grows. Instead, we can select the desired text ([Section 2.4](https://www.learnenough.com/text-editor-tutorial#sec-selecting_text)) and use a menu item or keyboard shortcut to comment out the selection. In Atom, we can comment out lines 2–3 by selecting those lines ([Figure 57](https://www.learnenough.com/text-editor-tutorial#fig-selecting_to_comment_out)) and hitting ⌘/, as shown in [Figure 58](https://www.learnenough.com/text-editor-tutorial#fig-commented_out). (Note from [Figure 58](https://www.learnenough.com/text-editor-tutorial#fig-commented_out) that the subtle save indicator shown in [Figure 43](https://www.learnenough.com/text-editor-tutorial#fig-saved_file) has been filled in; this is because I habitually press ⌘S after making changes, as recommended in [Section 2.7](https://www.learnenough.com/text-editor-tutorial#sec-saving).)

![images/figures/selecting_to_comment_out](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uwpnukzj30jg0kqzla.jpg)

Figure 57: Preparing to comment out some lines.

![images/figures/commented_out](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uwvxsg4j30jg0kqq3x.jpg)

Figure 58: Commented-out lines.

The commenting-out feature typically [toggles](https://en.wiktionary.org/wiki/toggle) back and forth, so by hitting ⌘/ a second time we can restore the file to its previous state ([Figure 57](https://www.learnenough.com/text-editor-tutorial#fig-selecting_to_comment_out)). This is useful when restoring some commented-out text after, for example, doing some debugging.

#### [Indenting and dedenting](https://www.learnenough.com/text-editor-tutorial#sec-indenting_and_dedenting)

Another element of code formatting made easier by text editors is *indentation*, which consists of the leading spaces at the beginning of certain lines.[23](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-23) For example, Ruby typically uses two spaces for indentation:

```
def hello(location)
  puts "hello, #{location}!"
end

```

In most languages, this is equivalent to the following:

```
def hello(location)
puts "hello, #{location}!"
end

```

This second example is harder to read, though, and it’s generally important to indent properly for the sake of humans reading the code even if the programming language doesn’t care.[24](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-24)

Text editors help maintain proper indentation in two main ways. First, new lines are typically inserted at the same level of indentation as the previous line, which you can verify by going to the end of line 3 in [Listing 15](https://www.learnenough.com/text-editor-tutorial#code-ruby_hello) and typing in the following two lines:

```
puts "Uh, oh."
puts "Goodbye, #{location}!"

```

The result appears in [Figure 59](https://www.learnenough.com/text-editor-tutorial#fig-indented_lines).

![images/figures/indented_lines](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uwy6rcdj30jg0kq75i.jpg)

Figure 59: Adding two indented lines.

The second main way text editors help maintain good code formatting is by supporting block indentation, which works in much the same way as commenting out code blocks. Suppose, for example, that (contrary to conventional Ruby practices) we decided to indent lines 3–5 in [Figure 59](https://www.learnenough.com/text-editor-tutorial#fig-indented_lines) six extra spaces, making eight spaces total. As with commenting out, the first step is to select the text we want to indent ([Figure 60](https://www.learnenough.com/text-editor-tutorial#fig-selecting_to_indent)). We can then type the tab key ⇥ to indent one “soft tab” (which is usually two spaces for Ruby) at a time. (If for any reason the default indentation in your editor doesn’t match the convention for the language you’re using, apply your technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) to figure out how to change it.) The result of applying three tabs in succession is shown in [Figure 61](https://www.learnenough.com/text-editor-tutorial#fig-indented).

![images/figures/selecting_to_indent](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ux0cm8kj30jg0kqgmu.jpg)

Figure 60: Preparing to indent some lines.

![images/figures/indented](https://ws1.sinaimg.cn/large/006tNc79gy1fm6ux2l9rnj30jg0kqgmu.jpg)

Figure 61: A block of Ruby code indented more than usual.

Because each extra tab just indents the block more, we can’t use the same command to undo indentation the way we did when commenting out code. Instead, we need to use a separate “dedent” command, which in Atom is ⇧⇥. Applying this command three times in succession returns us to our original state, as shown in [Figure 62](https://www.learnenough.com/text-editor-tutorial#fig-dedented). (By the way, many editors (including Atom) support the alternate keyboard shortcuts ⌘] and ⌘[ for indenting and dedenting, respectively.)

![images/figures/dedented](https://ws4.sinaimg.cn/large/006tNc79gy1fm6ux4y4yij30jg0kqgmu.jpg)

Figure 62: Dedenting the code block in [Figure 61](https://www.learnenough.com/text-editor-tutorial#fig-indented).

#### [Goto line number](https://www.learnenough.com/text-editor-tutorial#sec-goto_line_number)

It’s often important to be able to go to a particular line number, such as when debugging program that an error on (say) line 187. We saw this feature in [Section 1.5](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files), where we learned that the Vim command `<n>G` takes us to line `<n>`. In many other editors, the relevant shortcut is ⌃G. This opens a modal box where you can type in the line number, as shown in [Figure 63](https://www.learnenough.com/text-editor-tutorial#fig-line_number_box). (Incidentally, the syntax `:<number>` shown in [Figure 63](https://www.learnenough.com/text-editor-tutorial#fig-line_number_box), which is for Sublime Text, also works in Vim.)

![images/figures/line_number_box](https://ws3.sinaimg.cn/large/006tNc79gy1fm6ux6bm1ij30f301fq2v.jpg)

Figure 63: The modal box for going to a particular line number.

#### [80 columns](https://www.learnenough.com/text-editor-tutorial#sec-80_columns)

Finally, many text editors help programmers enforce a line limit of 80 characters across, usually called an “80-column limit”. Not all programmers observe this limit, but keeping our code to 80 columns makes it easier to read and display, for example in fixed-width terminals, blog posts, or tutorials such as this one. An 80-column limit also enforces good coding discipline, as exceeding 80 columns is often a sign that we would do well to introduce a new variable or function name.(The main exception to the 80-column rule is markup like HTML, Markdown, or LATEX, which is why in these cases we often activate word wrap as in [Section 2.2](https://www.learnenough.com/text-editor-tutorial#sec-opening).) Because it’s difficult to tell at a glance if a particular line exceeds 80 characters, many editors (including Atom and Sublime Text) include the option to display a subtle vertical line showing where the limit is, as shown in [Figure 64](https://www.learnenough.com/text-editor-tutorial#fig-eighty_columns).[25](https://www.learnenough.com/text-editor-tutorial#cha-0_footnote-25) If the 80-column limit indicator isn’t shown by default in your editor, flex your technical sophistication to figure out how to enable it. (It’s often associated with a setting called “word wrap column”.)

![images/figures/eighty_columns](https://ws4.sinaimg.cn/large/006tNc79gy1fm6ux82vy7j30j106cdg1.jpg)

Figure 64: Unsubtle arrows pointing at the subtle 80-column indicator in Atom.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_source_code)

1. Create the file `foo.rb`, then define the class `FooBar` ([Listing 16](https://www.learnenough.com/text-editor-tutorial#code-foobar_class)) using a tab trigger.*Hint*: Chances are the trigger is something like `cla⇥`.
2. Referring to [Listing 17](https://www.learnenough.com/text-editor-tutorial#code-foobar_new), add the definition of `bazquux` using the `def⇥` trigger, then add the final line shown by using autocomplete to type `FooBar` and `bazquux`. (Type the interstitial `.new.` by hand.)
3. Using tab triggers and autocomplete, make a file called `greeter.rb` with the contents shown in [Listing 18](https://www.learnenough.com/text-editor-tutorial#code-proto_greeter).
4. By cutting and pasting the text for the `hello` definition and indenting the block, transform [Listing 18](https://www.learnenough.com/text-editor-tutorial#code-proto_greeter) into [Listing 19](https://www.learnenough.com/text-editor-tutorial#code-greeter).

Listing 16: Creating a class using a tab trigger.`~/foo.rb`

```
class FooBar

end

```

Listing 17: Using autocomplete to make a class name.`~/foo.rb`

```
class FooBar
  def bazquux
    puts "Baz quux!"
  end
end

FooBar.new.bazquux

```

Listing 18: A proto-Greeter class in Ruby.`~/greeter.rb`

```
class Greeter
end

def hello(location)
  puts "hello, #{location}!"
end

Greeter.new.hello("world")

```

Listing 19: A completed Greeter class in Ruby.

```
class Greeter
  def hello(location)
    puts "hello, #{location}!"
  end
end

Greeter.new.hello("world")

```

### [3.3Writing an executable script](https://www.learnenough.com/text-editor-tutorial#sec-writing_an_executable_script)

As a practical application of the material in [Section 3.2](https://www.learnenough.com/text-editor-tutorial#sec-writing_source_code), in this section we’re going to write something that’s actually useful: a *shell script* designed to kill a program as safely as possible. (A *script* is a program that is typically used to automate common tasks, but the [detailed definition](https://en.wikipedia.org/wiki/Scripting_language)isn’t important at this stage.) En route, we’ll cover the steps needed to add this script to our command-line shell.

As [discussed](https://www.learnenough.com/command-line-tutorial#aside-ps_aux) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial), Unix user and system tasks take place within a well-defined container called a *process*. Sometimes, one of these processes will get stuck or otherwise misbehave, in which case we might need to terminate it with the `kill`command, which sends a *terminate code* to kill the process with a given id:

```
$ kill -15 12241

```

(See the [discussion](https://www.learnenough.com/command-line-tutorial#aside-ps_aux) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial) for more on how to find this id on your system.) Here we’ve used the terminate code `15`, which attempts to kill the process as gently as possible (meaning it gives the process a chance to clean up any temporary files, complete any necessary operations, etc.). Sometimes terminate code `15` isn’t enough, though, and we need to escalate the level of urgency until the process is well and truly dead. It [turns out](http://unix.stackexchange.com/a/8927) that a good sequence of codes is `15`, `2`, `1`, and `9`. Our task is to write a command to implement this sequence, which we’ll call `ekill` (for “escalating kill”), so that we can kill a process as shown in [Listing 20](https://www.learnenough.com/text-editor-tutorial#code-ekill_example).

Listing 20: An example of using `ekill` (to be defined).

```
$ ekill 12241

```

As with the Ruby example in [Section 3.2](https://www.learnenough.com/text-editor-tutorial#sec-writing_source_code), don’t worry about the details of the code; focus instead on the mechanics of the text editing.

As preparation for adding `ekill` to our system, we’ll first make a new directory in our home directory called `bin` (for “binary”):

```
$ mkdir ~/bin

```

(It’s possible that this directory already exists on your system, in which case you’ll get a harmless warning message.) We’ll then change to the `bin` directory and open a new file called `ekill`:

```
$ cd ~/bin
$ atom ekill

```

The `ekill` script itself starts with a “shebang” line (pronounced “she-BANG”, from “shell” and “bang”, with the latter being the [common pronunciation](https://www.learnenough.com/command-line-tutorial#aside-repeating_commands) of the exclamation mark `!`):

```
#!/bin/bash

```

This line tells our system to use the shell program located in `/bin/bash` to execute the script.By default, this program is the Bourne shell, or Bash, and in this context a shell script is often called a *Bash script*. Despite appearances, here the hash symbol `#` is *not* a comment character, which is potentially confusing because (as in Ruby) `#` is the character ordinarily used for a Bash comment line. Indeed, the initial version of our script includes several comment lines, as shown in [Listing 21](https://www.learnenough.com/text-editor-tutorial#code-custom_kill_script).

Listing 21: A custom escalating kill script.`~/bin/ekill`

```
1 #!/bin/bash
2
3 # Kill a process as safely as possible.
4 # Tries to kill a process using a series of signals with escalating urgency.
5 # usage: ekill <pid>
6
7 # Assign the process id to the first argument.
8 pid=$1
9 kill -15 $pid || kill -2 $pid || kill -1 $pid || kill -9 $pid

```

Apart from the shebang in line 1, all other uses of `#` introduce comments. Then, Line 8 assigns the process id `pid` to `$1`, which in a shell script is the first argument to the command, e.g., `12241` in [Listing 20](https://www.learnenough.com/text-editor-tutorial#code-ekill_example). Line 9 then uses the “or” operator `||` to execute the `kill` command using the code `15` or `2` or `1` or `9`, stopping on the first successful `kill`. (Again, don’t worry if you find this confusing; I include the explanation for completeness, but at this stage there’s no need to understand the details.)

After typing the contents of [Listing 21](https://www.learnenough.com/text-editor-tutorial#code-custom_kill_script) into the script file, one thing you might notice is that the result has no syntax highlighting, as seen in [Figure 65](https://www.learnenough.com/text-editor-tutorial#fig-kill_no_highlighting). This is because, unlike `README.md` in [Section 2.2](https://www.learnenough.com/text-editor-tutorial#sec-opening) and `hello.rb` in [Section 3.2](https://www.learnenough.com/text-editor-tutorial#sec-writing_source_code), the name `ekill` has no filename extension.Although some people would use a name like `ekill.sh` for shell scripts like this one—which would in fact allow our editor to highlight the syntax automatically—using an explicit extension on a shell script is a bad practice because the script’s name is the user interface to the program.As users of the system, we don’t care if `ekill` is written in Bash or Ruby or C, so calling it `ekill.sh` unnecessarily exposes the implementation language to the end-user. Indeed, if we wrote the first implementation in Bash but then decided to rewrite it in Ruby and then in C, every program (and programmer) using the script would have to change the name from `ekill.sh` to `ekill.rb` to `ekill.c`—an annoying and avoidable complication.

![images/figures/kill_no_highlighting](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uxams6mj30jg0kqwgd.jpg)

Figure 65: The `ekill` script with no syntax highlighting.

Even though we’ve elected not to use a filename extension for the `ekill` script, we’d still like to get syntax highlighting to work. One way is to click on “Plain Text” in the lower right-hand corner of the editor ([Figure 65](https://www.learnenough.com/text-editor-tutorial#fig-kill_no_highlighting)) and change the highlighting language to the one we’re using. This requires us to *know* the language, though, and it would be nicer if we could get the editor to figure it out automatically. Happily, we can arrange exactly that, simply by closing the file and opening it again. To do this, click on the X to close the `ekill` tab (or press ⌘W) and then re-open it from the command line:

```
$ atom ekill

```

Because of the shebang line in [Listing 21](https://www.learnenough.com/text-editor-tutorial#code-custom_kill_script), Atom infers that the file is a Bash script. As a result, the detected file type changes from “Plain Text” to “Shell Script”, and syntax highlighting is activated ([Figure 66](https://www.learnenough.com/text-editor-tutorial#fig-kill_with_highlighting)).

![images/figures/kill_with_highlighting](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uxdocg1j30jg0kq0uj.jpg)

Figure 66: The `ekill` script with syntax highlighting and a new detected file type.

At this point, we have a complete shell script, but typing `ekill <pid>` at the command line still won’t work. To add `ekill` to our system, we need to do two things:

1. Make sure the `~/bin` directory is on the system *path*, which is the set of directories where the shell program searches for *executable* scripts.
2. Make the script itself executable.

The list of directories on the path can be accessed via the special `$PATH` variable at the command line:

```
$ echo $PATH

```

If `~/bin` is on the list, you can skip this step, but it does no harm to follow it.

*Note*: The literal directory `~/bin` won’t appear in the `$PATH` list; instead the tilde will be expanded to your particular home directory. For me, `~/bin` is the same as `/Users/mhartl/bin`, so that’s what appears in my `PATH`, but it will be different for you.

To make sure `~/bin` is on the path, we’ll edit the Bash profile file we saw in [Section 1.2](https://www.learnenough.com/text-editor-tutorial#sec-editing_small_files). Open `~/.bash_profile` as follows:

```
$ atom ~/.bash_profile

```

Then add the `export` line shown in [Listing 22](https://www.learnenough.com/text-editor-tutorial#code-export_path).

Listing 22: Adding `~/bin` to the path.`~/.bash_profile`

```
alias lr='ls -hartl'
export PATH="~/bin:$PATH"

```

This uses the Bash `export` command to add `~/bin` to the current path. (It’s worth noting that some systems use the [*environment variable*](https://www.cyberciti.biz/faq/set-environment-variable-unix/) `$HOME` in place of `~`, but the two are synonyms. If for any reason `~` doesn’t work for you, it’s worth trying `$HOME` instead, as in `$HOME/bin:$PATH`.)

To use it, we need to use `source` as in [Section 1.3](https://www.learnenough.com/text-editor-tutorial#sec-saving_and_quitting_files):

```
$ source ~/.bash_profile

```

To make the resulting script executable, we need to use the “change mode” command `chmod` to add the “execute bit” `x` as follows:

```
$ chmod +x ~/bin/ekill

```

At this point, we can verify that the `ekill` script is ready to go using the `which` command:

```
$ which ekill

```

(This command is [covered](https://www.learnenough.com/command-line-tutorial#sec-downloading_a_file) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial).) The result should be the full path to `ekill`, which on my system looks like this:

```
/Users/mhartl/bin/ekill

```

As you can see by typing `ekill` by itself at the command line, the current behavior is confusing if we neglect to include a process id:

```
$ ekill
<confusing error message>

```

To make `ekill` friendlier in this case, we’ll arrange to print a usage message to the screen if the user neglects to include a process id. We can do this with the code in [Listing 23](https://www.learnenough.com/text-editor-tutorial#code-enhanced_kill_script), which I recommend typing in rather than copying and pasting. When writing the `if` statement, I especially recommend trying `if`⇥ to see if your editor comes with a tab trigger for making Bash `if` statements.

Listing 23: An enhanced version of the escalating kill script.`~/bin/ekill`

```
#!/bin/bash

# Kill a process as safely as possible.
# Tries to kill a process using a series of signals with escalating urgency.
# usage: ekill <pid>

# If the number of argument is less than 1, exit with a usage statement.
if [[ $# -lt 1 ]]; then
  echo "usage: ekill <pid>"
  exit 1
fi

# Assign the process id to the first argument.
pid=$1
kill -15 $pid || kill -2 $pid || kill -1 $pid || kill -9 $pid

```

After adding the code in [Listing 23](https://www.learnenough.com/text-editor-tutorial#code-enhanced_kill_script), running `ekill` without an argument should produce a helpful message:

```
$ ekill
usage: ekill <pid>

```

All we have left to do is to verify that `ekill` can actually be used to kill a process. This is left as an exercise ([Section 3.3.1](https://www.learnenough.com/text-editor-tutorial#sec-exercises_script).)

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_script)

1. Let’s test the functionality of `ekill` by making a process that hangs and applying the lessons from [grepping processes](https://www.learnenough.com/command-line-tutorial#aside-ps_aux) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial). We’ll start by opening two terminal tabs. In one tab, type `tail` to get a process that just hangs.In the other tab, use `ps aux | grep tail` to find the process id, then run `ekill <pid>` (substituting the actual id for `<pid>`). In the tab running `tail`, you should get something like “Terminated: 15” ([Figure 67](https://www.learnenough.com/text-editor-tutorial#fig-killed_tail)).
2. Write an executable script called `hello` that takes in an argument and prints out “Hello” followed by the argument. Be sure to `chmod` the script so it can run properly.*Hint*: Use the `echo` command. *Bigger hint*: Bash scripts *interpolate* dollar-sign variables into strings, so the `$1` variable from [Listing 21](https://www.learnenough.com/text-editor-tutorial#code-custom_kill_script) can be used in a string like this: `"Hello, $1"`

![images/figures/killed_tail](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uxftyu5j30jg0fq74u.jpg)

Figure 67: The result of using `ekill` to kill a `tail` process.

### [3.4Editing projects](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects)

So far we’ve used our text editor to edit single files, but it can also be used to edit entire projects all at once. As an example of such a project, we’ll download the sample application from the 3rd edition of the [*Ruby on Rails Tutorial*](http://railstutorial.org/book). We won’t be running this application, but it will give us a large project to work with. As in [Section 1.5](https://www.learnenough.com/text-editor-tutorial#sec-editing_large_files) and [Section 2.2](https://www.learnenough.com/text-editor-tutorial#sec-opening), we’ll use the `curl` command to download the file to our local disk:

```
$ cd
$ curl -OL source.railstutorial.org/sample_app.zip

```

As indicated by the `.zip` filename extension, this is a ZIP file, so we’ll unzip it (using the `unzip` command) and then `cd` into the sample app directory:

```
$ unzip sample_app.zip
   creating: sample_app_3rd_edition-master/
   .
   .
   .
$ cd sample_app_3rd_edition-master/

```

The way to open a project is to use a text editor to open the entire directory. Recall (from, e.g., [navigating directories](https://www.learnenough.com/command-line-tutorial#sec-navigating_directories) in [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial)) that `.` (“dot”) is the current directory, which means that we can open it using “atom dot”:

```
$ atom .

```

The resulting text editor window includes the directory structure for our project, called a “tree view”, as seen in [Figure 68](https://www.learnenough.com/text-editor-tutorial#fig-atom_sample_app). We can toggle its display using the View menu or a keyboard shortcut ([Figure 69](https://www.learnenough.com/text-editor-tutorial#fig-atom_sample_app_no_tree_view)).

![images/figures/atom_sample_app](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uxhmg10j30jg0kqmyr.jpg)

Figure 68: The Rails Tutorial sample app in Atom.

![images/figures/atom_sample_app_no_tree_view](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uxjhxyfj30jg0kcdgi.jpg)

Figure 69: Toggling the tree view.

#### [Fuzzy opening](https://www.learnenough.com/text-editor-tutorial#sec-fuzzy_opening)

It’s possible to open a file by double-clicking on it in the tree view, but in a project with a lot of files this is often cumbersome, especially when the file is buried several subdirectories deep. A convenient alternative is *fuzzy opening*, which lets us open files by hitting (in Atom) ⌘P and then typing some of the letters in the filename we want. For example, we can open a file called `users_controller_test.rb` by typing, say, “userscon” and then selecting from the drop-down menu, as shown in [Figure 70](https://www.learnenough.com/text-editor-tutorial#fig-fuzzy_one). The letters don’t have to be sequential in the filename, though, so typing “uctt” (for **u**sers **c**on**t**roller **t**est) will also work, as seen in [Figure 71](https://www.learnenough.com/text-editor-tutorial#fig-fuzzy_two).

![images/figures/fuzzy_one](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uxkzqcbj30jg0k4myb.jpg)

Figure 70: One way to open a file with fuzzy opening.

![images/figures/fuzzy_two](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uxmwhbdj30jg0k4abu.jpg)

Figure 71: A second way to open a file with fuzzy opening.

As a result of opening multiple files in a project, you will generally have multiple tabs open in your editor ([Figure 72](https://www.learnenough.com/text-editor-tutorial#fig-multiple_tabs)). I recommend learning the keyboard shortcuts to switch between them, which are typically things like ⌘1, ⌘2, etc. (By the way, this trick also works in many browsers, such as Chrome and Firefox.)

![images/figures/multiple_tabs](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uxr28wrj30jg0kcgq3.jpg)

Figure 72: Opening multiple tabs.

#### [Multiple panes](https://www.learnenough.com/text-editor-tutorial#sec-multipile_panes)

The default editor view we’ve seen in most of the previous examples consists of a single *pane* (as in “window pane”), but it’s often convenient to split the editor into multiple panes so that we can see more than one file at a time ([Figure 73](https://www.learnenough.com/text-editor-tutorial#fig-multiple_panes)). I especially like to use different panes for different types of files, such as using the left pane for test code and the right pane for application code. It’s also often useful to open the same file in two different panes ([Figure 74](https://www.learnenough.com/text-editor-tutorial#fig-same_file_different_panes)); as I wrote in the meta-tutorial [*Learn Enough Tutorial Writing to Be Dangerous*](http://www.learnenough.com/tutorial-writing-tutorial):

> When searching through the document for whatever reason (to fix an error, look up a label for a cross-reference, find a particular string, etc.), it’s usually inconvenient to move the cursor and hence lose our place. In this context, it’s useful to have the same file open in two different text editor windows… This way, we can use one pane as the main writing area and the other pane as a sort of “random access” window for moving around in the document.

![images/figures/multiple_panes](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uxtgpkij30jg0b341r.jpg)

Figure 73: Using multiple panes.

![images/figures/same_file_different_panes](https://ws2.sinaimg.cn/large/006tNc79gy1fm6uxw53lej30jg0bqjxc.jpg)

Figure 74: Opening the same file in two different panes.

#### [Global find and replace](https://www.learnenough.com/text-editor-tutorial#sec-global_find_and_replace)

We saw in [Section 2.8](https://www.learnenough.com/text-editor-tutorial#sec-finding_and_replacing) how to find and optionally replace content in a single file. When editing projects, it’s often useful to be able to do a *global* find and replace across multiple files. As usual, most editors have both a menu item ([Figure 75](https://www.learnenough.com/text-editor-tutorial#fig-find_in_project_menu_item)) and a keyboard shortcut (often ⇧⌘F).

![images/figures/find_in_project_menu_item](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uxyfg67j306n09k74s.jpg)

Figure 75: A menu item for global find and replace.

An example of global find appears in [Figure 76](https://www.learnenough.com/text-editor-tutorial#fig-find_in_project), which searches for the string “@user” in all project files. The command to globally replace this with “@person” appears in [Figure 77](https://www.learnenough.com/text-editor-tutorial#fig-replace_in_project).

![images/figures/find_in_project](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uy0nqm7j30jg0bb779.jpg)

Figure 76: The result of finding in project.

![images/figures/replace_in_project](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uy2iww9j30jg0bbad4.jpg)

Figure 77: The result of replacing in project.

One thing to bear in mind when using global find and replace is that it can be hard to undo. In the case of a single file, it’s easy enough to undo a bad replacement with ⌘Z ([Section 2.6](https://www.learnenough.com/text-editor-tutorial#sec-deleting_and_undoing)), but when replacing across multiple files we have to run ⌘Z in *every* affected file, which could be dozens. As a result, I recommend using global find and replace with great caution, and preferably in combination with a version control system such as Git. My practice is to make a *commit* before any global search and replace so that I can easily undo it if there turns out to be a mistake. (See [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial) for more information.)

By the way, for really advanced replacing we can use *regular expressions* (or *regexes*), which are often indicated with a menu item that looks like `.*`. Regexes are covered in more detail in [*Learn Enough Regular Expressions to Be Dangerous*](http://www.learnenough.com/regular-expressions-tutorial). If you decide to experiment with regular expression searches, I also recommend playing around with the outstanding [Rubular](http://rubular.com/) regular expression builder.

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_project)

1. What is the keyboard shortcut in your editor for toggling the tree view?
2. What is the keyboard shortcut in your editor for splitting panes horizontally?
3. In the Rails Tutorial sample app project, open the file `static_pages_controller.rb`using fuzzy opening.
4. Use global find to find all occurrences of the string `@user`.
5. Use global replace to change all occurrences of `@user` to `@person`.

### [3.5Customization](https://www.learnenough.com/text-editor-tutorial#sec-customization)

All good text editors are highly customizable, but the options are highly editor-dependent. The most important things are (a) to know what kind of customization is possible and (b) to apply your technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) to figure out how to make the desired changes.

For example, one student of the [Ruby on Rails Tutorial](http://railstutorial.org/) wrote in asking about the dark background in the Cloud9 editor (e.g., [Figure 17](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_filesystem_navigator)), wondering if it was possible to use a light background instead. I responded that it was almost certainly possible to change to a light background, even though I didn’t know how to do it offhand. I knew that every good programmer’s editor has multiple highlighting color schemes, font sizes, tab sizes, etc., so I was confident I could figure out how to change the background color on the Cloud9 editor. And indeed, by clicking around and looking for promising menu items (a textbook application of [Figure 3](https://www.learnenough.com/text-editor-tutorial#fig-tech_support_cheat_sheet)), I was able to discover the answer (Preferences > Themes > Syntax Theme > Cloud9 Day), as shown in [Figure 78](https://www.learnenough.com/text-editor-tutorial#fig-cloud9_light_background).

![images/figures/cloud9_light_background](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uy5wsraj30jg0eogp5.jpg)

Figure 78: The Cloud9 editor with a light background.

Another feature common to good text editors is some sort of package system. For example, we saw in [Section 2.2.2](https://www.learnenough.com/text-editor-tutorial#sec-previewing_markdown) that Atom comes with a built-in package to preview Markdown, but in Sublime Text we need to install a separate package to do it. One way to find new packages is to [Google around](http://lmgtfy.com/?q=sublime+text+package+search) for more information, leading to a site like that shown in [Figure 79](https://www.learnenough.com/text-editor-tutorial#fig-package_search). By clicking around the Sublime menu items, we can also find Sublime Text > Preferences > Package Control, as shown in [Figure 80](https://www.learnenough.com/text-editor-tutorial#fig-package_control_menu) and [Figure 81](https://www.learnenough.com/text-editor-tutorial#fig-package_control).

![images/figures/package_search](https://ws1.sinaimg.cn/large/006tNc79gy1fm6uy8dubsj30jg0eo78p.jpg)

Figure 79: Searching for a Sublime Text package.

![images/figures/package_control_menu](https://ws3.sinaimg.cn/large/006tNc79gy1fm6uya5zhsj306907zt96.jpg)

Figure 80: Sublime Text’s Package Control menu item.

![images/figures/package_control](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uybw8dsj30gk0dgtbg.jpg)

Figure 81: Sublime Text’s Package Control.

Most editors allow you to create your own packages of commands, as well as often supporting *snippets* that let you define your own tab triggers ([Section 3.1](https://www.learnenough.com/text-editor-tutorial#sec-autocomplete_tab_triggers)). These are advanced topics, so I recommend deferring them for now. Once you start becoming annoyed by having to repeatedly type the same boilerplate (as in, e.g., [Listing 24](https://www.learnenough.com/text-editor-tutorial#code-listing_boilerplate)), [Google around](http://lmgtfy.com/?q=atom+custom+snippets) to figure out how to add custom commands to your editor. (The code in [Listing 24](https://www.learnenough.com/text-editor-tutorial#code-listing_boilerplate) is generated using the custom Sublime Text tab trigger `clist` (for “code listing”), which I have also [ported](https://en.wikipedia.org/wiki/Porting) to Atom.)

Listing 24: The boilerplate for a code listing in this document.

```
\begin{codelisting}
\label{code:}
\codecaption{}
%= lang:
\begin{code}

\end{code}
\end{codelisting}

```

#### [Exercises](https://www.learnenough.com/text-editor-tutorial#sec-exercises_customization)

1. Figure out how to change the syntax highlighting theme in your editor. Use the file from [Listing 19](https://www.learnenough.com/text-editor-tutorial#code-greeter) to confirm the change.
2. In Atom, figure out how to install the `minimap` package. What does this package do?The result for `sonnets.txt` should look something like [Figure 82](https://www.learnenough.com/text-editor-tutorial#fig-atom_minimap).

![images/figures/atom_minimap](https://ws4.sinaimg.cn/large/006tNc79gy1fm6uyfspirj30jg0jkqa7.jpg)

Figure 82: The result of adding `minimap` to Atom.

### [3.6Summary](https://www.learnenough.com/text-editor-tutorial#sec-summary_advanced_text_editing)

- Autocomplete and tab triggers make it easy to type lots of text quickly.
- All good text editors have special features to support writing computer source code, including syntax highlighting, commenting out, indenting & dedenting, and goto line number.
- Many programmers think it’s perfectly fine to have lines that are more than 80 columns across, but they are wrong. (Speaking of which, there’s nothing quite so entertaining as a holy war ([Box 5](https://www.learnenough.com/text-editor-tutorial#aside-holy_wars))…)
- Once you know how to use the command line and a text editor, it’s easy to add custom shell scripts to your system.
- It’s common to open entire projects (such as Ruby on Rails applications) all at once using the command line.
- Fuzzy opening is useful when editing projects with large numbers of files.
- Using multiple panes allows the editor to display more than one file at a time.
- Global find and replace is dangerous but powerful.
- All good programmer’s editors are extensible and customizable.

Important commands from this section are summarized in [Table 4](https://www.learnenough.com/text-editor-tutorial#table-advanced_text_editing).

| **Command**              | **Description**            |
| ------------------------ | -------------------------- |
| Select + ⌘/              | Toggle commenting out      |
| Select + ⇥               | Indent                     |
| Select + ⇧⇥              | Dedent                     |
| ⌃G                       | Goto line number           |
| ⌘W                       | Close a tab                |
| `$ echo $PATH`           | Show the current path      |
| `$ chmod +x <filename>`  | Make `filename` executable |
| `$ unzip <filename>.zip` | Unzip a ZIP archive        |
| ⌘P                       | Fuzzy opening              |
| ⌘1                       | Switch focus to tab #1     |
| ⇧⌘F                      | Global find and replace    |

Table 4: Important commands from [Section 3](https://www.learnenough.com/text-editor-tutorial#sec-advanced_text_editing).

## [4Conclusion](https://www.learnenough.com/text-editor-tutorial#sec-conclusion)

Congratulations! You now know enough text editor to be *dangerous*. If you continue down this technical path, you’ll keep getting better at using text editors for years to come, but with the material in this tutorial you’ve got a great start. For now, you’re probably best off working with what you’ve got, applying your technical sophistication ([Box 3](https://www.learnenough.com/text-editor-tutorial#aside-technical_sophistication)) when necessary. Once you’ve got a little more experience under your belt, I recommend seeking out resources specific to your editor of choice. To get you started, here are some links to documentation for the editors mentioned in this tutorial:

- [*Learn Enough Vim to Be Dangerous*](http://learnenough.com/vim-tutorial)
- [Atom docs](https://atom.io/docs)
- [Sublime Text docs](https://www.sublimetext.com/docs/3/)
- [Cloud9 editor docs](https://docs.c9.io/docs/the-editor)

As a reminder, *Learn Enough Text Editor to Be Dangerous* is just one in a [series of tutorials](http://learnenough.com/#coming_soon)designed to teach the fundamentals of software development. The next step in the series is [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial), and the full sequence appears as follows:

1. Developer Fundamentals
   1. [*Learn Enough Command Line to Be Dangerous*](http://www.learnenough.com/command-line-tutorial)
   2. [*Learn Enough Text Editor to Be Dangerous*](http://www.learnenough.com/text-editor-tutorial) (you are here)
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

Good luck!

*Learn Enough Text Editor to Be Dangerous*. Copyright © 2015 by Michael Hartl.
