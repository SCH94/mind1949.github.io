---
layout: post
title: "Learn Enough HTML to Be Dangerous"
date: 2017-12-5
tags:
  Learn_Enough
  Html
  教材
---
![cover](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ci3v5dj30fi0ncq3q.jpg)

# Learn Enough HTML to Be Dangerous**Michael Hartl and Lee Donahoe**

A tutorial introduction to HTML

+

$9.00

Buy eBook

Also available: over an hour of instructional screencasts that walk you step by step through the tutorial

[** Mailing List](https://www.learnenough.com/html-tutorial) [** All Access Subscription](https://www.learnenough.com/subscribe)

HyperText Markup Language, or *HTML* for short, is the universal language of the World Wide Web. Every time you visit a website, the site’s web server sends HTML to your browser, which then renders it as the web page you see on your screen. Because this process is universal, anyone who works with web technologies—which these days means virtually all developers, designers, and even many managers—can benefit from knowing the basics of what HTML is and how it works. *Learn Enough HTML to Be Dangerous* is designed to give you this foundation in basic HTML.

Appropriately enough, there are lots of HTML tutorials on the Web, but most of them use toy examples, focusing on HTML syntax in isolation, without showing how HTML is written and deployed in real life. In contrast, *Learn Enough HTML to Be Dangerous* not only shows you how to make real HTML pages, it shows you how to deploy an actual site to the live Web. If you have previously attempted or completed an HTML tutorial, it’s likely that *Learn Enough HTML to Be Dangerous* will help you “put everything together” in a way you haven’t seen before, including an emphasis on expanding your skillset with *technical sophistication* ([Box 1](https://www.learnenough.com/html-tutorial#aside-technical_sophistication)).

At the same time, there are many HTML books on the market that are substantially too long for what is, at its core, a simple subject. You don’t need to master 500 pages of material to be highly productive with HTML. Thus, in keeping with the Learn Enough philosophy, this tutorial teaches only the most important aspects of the subject—enough to be *dangerous*.

> Box 1. Technical sophistication
>
> If tech is the new literacy, technical sophistication is like being able to read and write. This includes being able to figure things out on your own (like sounding out words while reading) and look things up when you need them (like consulting a dictionary or thesaurus while writing).
>
> On the Web, the alphabet is HTML.
>
> In *Learn Enough HTML to Be Dangerous*, we’ll constantly be on the lookout for chances to improve our technical sophistication. We’ll deploy our website immediately to production ([Section 1.2](https://www.learnenough.com/html-tutorial#sec-project_start)), getting over any bumps along the way.We’ll push ourselves to read HTML we don’t quite understand, content to get the gist at first before deepening our mastery later. And we’ll put all our tools to use, combining the [command line](http://learnenough.com/command-line-tutorial), [text editor](http://learnenough.com/text-editor-tutorial), and [version control](http://learnenough.com/git-tutorial) to learn how to make HTML websites the Right Way™—professional-grade from the start.
>

Because of our pragmatic approach, the tools we’ll be using are all professional-grade ([Figure 1](https://www.learnenough.com/html-tutorial#fig-tools_of_the_trade)). They are the same tools covered in the Learn Enough Developer Fundamentals sequence, which you should follow now if you’re not already familiar with them. The individual tutorials are available for free on the Web:

1. [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial) on the Unix command line
2. [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial) on text editors
3. [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial) on version control with Git

To get even more out of the sequence, you can join our subscription service, the [Learn Enough Society](http://learnenough.com/society), which includes streaming videos and special enhanced versions of the online tutorials, among other benefits.

![images/figures/tools_of_the_trade](https://ws3.sinaimg.cn/large/006tNc79gy1fm65cq0sq7j311y0lcwyi.jpg)

Figure 1: The tools of the trade (kitten not included).

If you’re just getting started with HTML, the Developer Fundamentals sequence represents a little bit of overhead, but the benefits are enormous. To our knowledge, this combination of software development best practices and deploying to a live website is unique among introductory HTML tutorials, and gives you a tremendous advantage both when collaborating with others and when taking your skills to the next level by learning to build more complicated sites.

*Learn Enough HTML to Be Dangerous* focuses on core HTML, starting with a “hello, world!” page that we’ll deploy to production (!) in [Section 1](https://www.learnenough.com/html-tutorial#sec-html_intro). We’ll then fill in the *index page* with formatted text, links, and images in [Section 2](https://www.learnenough.com/html-tutorial#sec-filling_in_the_index_page), expanding it into a multiple-page site with more advanced features like tables and lists in [Section 3](https://www.learnenough.com/html-tutorial#sec-more_pages). Finally, we’ll add some inline styling in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles), which will allow us to see the effect of simple style rules on plain HTML elements.

The resulting site will be functional, but we’ll run into several important limitations imposed by working with raw HTML. This will set the stage for the next Learn Enough tutorial, [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial), which creates a fully modern website using *Cascading Style Sheets* (CSS) to separate the design of the site from its HTML structure, while covering site layouts and advanced styling as well.

*Note*: The online version of this tutorial is available for free, and the ebook and videos are available for purchase [here](https://www.learnenough.com/buy/234).

## [1Basic HTML](https://www.learnenough.com/html-tutorial#sec-html_intro)

Underneath every website, no matter how simple or complex, you will find HTML. In this tutorial, by creating and deploying a simple but real website, we’ll gain an understanding of the underlying structure that every site uses to organize and display content online.

As a technology standard, HTML has been constantly evolving ever since its introduction in 1993 by Tim Berners-Lee, the original “web developer” ([Figure 2](https://www.learnenough.com/html-tutorial#fig-tim_berners_lee)).[1](https://www.learnenough.com/html-tutorial#cha-0_footnote-1) Nowadays, the specification of what’s in HTML and what isn’t is managed by the [World Wide Web Consortium (W3C)](http://www.w3.org/). The latest public release, which is what we will be using in this tutorial, is HTML5 (that is, version 5 of HTML). The companies that create web browsers take the specs from the W3C and implement the behaviors that are expected when the browser comes across any of the allowed formatting, such as **making text bold** or changing its color (or even **doing both** at the same time).

![images/figures/tim_berners-lee](https://ws3.sinaimg.cn/large/006tNc79gy1fm65d0mpekj30hs0buabj.jpg)

Figure 2: Sir Tim Berners-Lee, the original web developer.

Fortunately, we won’t need to get into a lot of specifics or worry about what has changed from version to version. Just know that new features are being added regularly to expand browser functionality and modernize the technology. Common elements, including the ones we’ll be covering in this tutorial, haven’t changed much since the beginning, but that doesn’t mean that they will always be safe—the HTML spec is a constantly evolving creature being assembled by a committee ([Figure 3](https://www.learnenough.com/html-tutorial#fig-camel)).[2](https://www.learnenough.com/html-tutorial#cha-0_footnote-2) We’ll discuss some practical effects of this in [Section 1.1](https://www.learnenough.com/html-tutorial#sec-html_tags).

![images/figures/camel](https://ws4.sinaimg.cn/large/006tNc79gy1fm65d64k4vj30kv0f5tfo.jpg)

Figure 3: HTML in animal form.

### [1.1HTML tags](https://www.learnenough.com/html-tutorial#sec-html_tags)

As the name **H**yper**T**ext **M**arkup **L**anguage indicates, HTML is a *markup* language, not a programming language. HTML allows a web author to organize and define how content should be displayed, which means it can do things like add text formatting; make headings, lists, and tables; and include images and links. You can think of an HTML file as an ordinary written document that has been carefully annotated by the author. Some of the notes might highlight parts of the text, some might include an image that has been paper-clipped to the document, and others might tell you where to find additional information.

The “HyperText” part of the HTML acronym refers to the way links on the Web allow you to move from one document to another in a non-linear fashion. For example, if you are reading the [Wikipedia article on HTML](https://en.wikipedia.org/wiki/HTML) and see a highlighted link to a related topic like [CSS](https://en.wikipedia.org/wiki/Cascading_Style_Sheets), you can click on that link and be taken immediately to the other article. It also allows a document like this one to link to [Wikipedia](http://wikipedia.org/). (You might notice that external links in this document open in a new browser tab. We’ll learn how to do this ourselves in [Section 3.3](https://www.learnenough.com/html-tutorial#sec-divs_and_spans).)

Technologically, hypertext is a great improvement over non-linked documents, as it eliminates the need to flip or scroll through pages of content to find what you are looking for. These days, the ability to link between documents is something that we all take for granted, but when the HTML specification was created it was an innovation important enough to be included in the name of the technology.

HTML source is *plain text*, which makes it ideal for editing with a text editor (as discussed in [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial)). Instead of using the convenient but inflexible What You See Is What You Get (WYSIWYG) approach of word processors, HTML indicates formatting using special *tags* ([Figure 4](https://www.learnenough.com/html-tutorial#fig-storm_trooper_tagged)),[3](https://www.learnenough.com/html-tutorial#cha-0_footnote-3) which are the text annotations alluded to above.

![images/figures/storm_trooper_tagged](https://ws1.sinaimg.cn/large/006tNc79gy1fm65d9fgbxj30hs0budgq.jpg)

Figure 4: HTML uses tags for everything.

As we’ll see, HTML supports more than one kind of tags, but the most common kind consist of strings (sequences of characters) enclosed in *beginning* and *ending* tags, like this:

```
<strong>make them strong</strong>

```

[Figure 5](https://www.learnenough.com/html-tutorial#fig-anatomy_of_a_tag) illustrates the detailed anatomy of this typical tag, including the name of the tag (`strong`, in this case), angle brackets, and a forward slash (`/`).

![images/figures/anatomy_of_a_tag](https://ws1.sinaimg.cn/large/006tNc79gy1fm65dbzffzj30vr0dwmy8.jpg)

Figure 5: The anatomy of a typical HTML tag.

Although HTML tags are not visible to the end-user (i.e., the person viewing your website), they do give the web browser suggestions about how to format the content and how it should be displayed on the page. A simple example using the `strong` tag appears in [Listing 1](https://www.learnenough.com/html-tutorial#code-first_example).

Listing 1: A string with HTML tags in the text.

```
I am a string about things. Some of those things are more important than others,
and I want to draw attention to them, so I will <strong>make them
strong</strong> so that they stand out among their less spectacular neighbors.

```

Most browsers render the `strong` tag as **boldface text**, so in a typical browser [Listing 1](https://www.learnenough.com/html-tutorial#code-first_example) would appear something like this:

> I am a string about things. Some of those things are more important than others, and I want to draw attention to them, so I will **make them strong** so that they stand out among their less spectacular neighbors.

Note that, even though the contents of the `strong` tag are broken across a line in [Listing 1](https://www.learnenough.com/html-tutorial#code-first_example), the browser ignores this extra space, and formats the string as a continuous line of text.

By the way, HTML does support a `b` (bold) tag in addition to `strong`, but over the years HTML has moved away from tag names that specify formatting (i.e., “make the text **bold**”) and toward names that focus on *meaning*—or, in fancier terms, [*semantics*](https://en.wikipedia.org/wiki/Semantics)—leading to an emphasis on so-called *semantic tags* ([Box 2](https://www.learnenough.com/html-tutorial#aside-semantic_tale)). For example, the semantic tag `strong` indicates that the enclosed text should be made to look “strong” somehow, letting the browser decide exactly how to do it.

> Box 2. The cautionary (semantic) tale of `<b>` and `<i>`
>
> When HTML was first created, the Internet made [funny noises](https://www.dialupsound.com/) when you connected to it, and you paid for the connection in time or by amount of data sent.Those limitations meant that brevity was an important consideration when deciding on tags, and the whole endeavor was so new that there wasn’t as much thought about the meaning the tags conveyed. So short tags were popular, and getting everything to display correctly to people was the end-goal.
>
> As a result of this focus on concision, the original way to make text bold was to use the `b` tag (`<b>...</b>`), and to make text italic it was the `i` tag (`<i>...</i>`). This worked just fine (in fact, it still works even today), and no one was confused.
>
> What some developers began to notice was that HTML tags were being defined only by how the content inside should be displayed in a browser, rather than by the meaning of the content. That’s fine for people looking at content with good ol’ eyeballs, but not so good for automated systems that might be rapidly scanning web pages and need to infer what the content wrapped in different HTML tags actually means.
>
> To address this issue, a movement started that pushed for new tags based on semantic meaning instead of on appearance, thereby giving rise to the current preferred method for indicating bold or italicized text with `strong`(`<strong>...</strong>`) and `em` (`<em>...</em>`, for “emphasized”), respectively. The idea here is that the intent behind making text bold is to make it strongly **stand out** from the rest of the content, and the intent behind italicizing text is to *show emphasis*.
>
> This might seem like a subtle difference, but semantic tags are used for a lot more than just defining strong or emphasized text. Semantic HTML tags will be further discussed in the [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial), where we will cover tag conventions and page layout in greater depth.
>

At this point, we’ve covered the conceptual core of HTML: HTML consists of text content wrapped in tags, which organize or indicate a change in the display of that content.

But the Devil, as they say, is in the details… and HTML has a whole lot of details.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_html_tags)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

*Note*: Unlike most other Learn Enough tutorials, the results of some exercises will appear in future screenshots.

1. Identify all the tags in [Listing 2](https://www.learnenough.com/html-tutorial#code-exercise_snippet). Notice that you don’t have to know what a tag does to be able to identify it correctly. (This is a good example of technical sophistication ([Box 1](https://www.learnenough.com/html-tutorial#aside-technical_sophistication)).)
2. Some HTML tags don’t contain any content, and instead are known as *void elements*, also called *self-closing tags*. Which tag in [Listing 2](https://www.learnenough.com/html-tutorial#code-exercise_snippet) is a void element?
3. HTML tags can be *nested*, which means that one tag can be put inside another.Which tags in [Listing 2](https://www.learnenough.com/html-tutorial#code-exercise_snippet) are nested? Don’t include any self-closing tags.

Listing 2: Shall I compare thee to a summer’s day?

```
<p>
  William Shakespeare's <em>Sonnets</em> consists of 154 poems, each fourteen
  lines long (three
  <a href="https://en.wikipedia.org/wiki/Quatrain">quatrains</a>
  followed by a rhyming
  <a href="https://en.wikipedia.org/wiki/Couplet">couplet</a>).
  <strong>Sonnet 18</strong> is perhaps the most famous, and begins like this:
</p>
<blockquote>
  <p>
    Shall I compare thee to a summer's day?<br>
    Thou art more lovely and more temperate.<br>
    Rough winds do shake the darling buds of May,<br>
    And summer's lease hath all too short a date.
  </p>
</blockquote>

```

### [1.2Starting the project](https://www.learnenough.com/html-tutorial#sec-project_start)

Now that we know the basic structure of markup and tags, it’s time to get started with the project that will serve as our sample website for learning HTML. The sample project is a mock informational website, whose main page talks a little about this tutorial, the company behind it, and HTML itself. As we develop the home page and two ancillary pages, we’ll see how to use a wide variety of HTML tags, while also showing you how to make the kind of public-facing site that you could use for your own work or as a service to other people. Although some of the information on the site is about Learn Enough to Be Dangerous, ultimately it is about *you*.

We’ll begin by following the same steps used in [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial), so this section will also serve as a review of how to use Git. (If you don’t have Git proficiency at the level of [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial), we recommend you read that tutorial at this time.) As in the Git tutorial, the result here will be that we can deploy our sample HTML site to the live Web using GitHub Pages ([Box 3](https://www.learnenough.com/html-tutorial#aside-github_pages)).

> Box 3. GitHub Pages
>
> Once you have an account at [GitHub](http://github.com/) (and have [verified your emailed address](https://help.github.com/articles/verifying-your-email-address/)), you can use a free feature called *GitHub Pages* that allows you to host simple HTML sites for free on GitHub’s infrastructure.
>
> This is a major advance compared to the bad old days of the early Web. For example, if this were 1999, you’d not only have to pay money for the hosting, but you’d also be on the hook for the cost of transferring the data to the people visiting your site. For sites with even moderate traffic, the bills could add up fast.
>
> Nowadays, we have many better options, GitHub Pages among them. Not only is GitHub Pages free, but it is incredibly easy to use. When you host a repo at GitHub, any valid HTML stored on the `gh-pages` branch of the repo is available online (nearly) instantly. All you need to do is commit your changes on the branch and push the commit to GitHub. GitHub Pages takes care of the rest.
>

We’ll get started by making a directory and an initial repository for our sample website.First, open a terminal window and make a directory called `sample_website`:[4](https://www.learnenough.com/html-tutorial#cha-0_footnote-4)

```
$ mkdir -p repos/sample_website

```

Next, `cd` into the directory and `touch` the file for the main page of the site, which should be called `index.html`:

```
$ cd repos/sample_website
$ touch index.html

```

Then initialize the repository:

```
$ git init
$ git add -A
$ git commit -m "Initialize repository"

```

The reason we created a file using `touch` is because Git won’t initialize an empty repository.[5](https://www.learnenough.com/html-tutorial#cha-0_footnote-5) The reason we’ve called it `index.html` is because that’s the default filename for “home” pages on the Web, and most sites will automatically serve up `index.html` when you hit the bare domain. In other words, when you point a browser at [example.com](http://example.com/), the server will automatically show you [example.com/index.html](http://example.com/index.html). (Those links work, by the way; amazingly, the HTML standard specifically reserves the site [example.com](http://example.com/) for examples just like this one!)

With the repo initialized, we’re now ready to push our (nearly) empty repo up to GitHub.As in [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial), you should go to [github.com](https://github.com/), log in if necessary, and then create a new repository using the name `sample_website` and the description “A sample website for Learn Enough HTML to Be Dangerous”, as shown in [Figure 6](https://www.learnenough.com/html-tutorial#fig-add_new_repository) and [Figure 7](https://www.learnenough.com/html-tutorial#fig-new_repo).[6](https://www.learnenough.com/html-tutorial#cha-0_footnote-6)

![images/figures/add_new_repository](https://ws4.sinaimg.cn/large/006tNc79gy1fm65de9gptj30a703874f.jpg)

Figure 6: The GitHub new repository menu.

![images/figures/new_repo](https://ws3.sinaimg.cn/large/006tNc79gy1fm65di7xcpj30vk0nttbz.jpg)

Figure 7: Creating a new GitHub repo for our website.

After creating the remote repo, you should set the *remote origin* as the main URL for the repo, which you can find as shown in [Figure 8](https://www.learnenough.com/html-tutorial#fig-repo_url):

```
$ git remote add origin <repo url>

```

![images/figures/repo_url](https://ws3.sinaimg.cn/large/006tNc79gy1fm65dto4tuj30vi0ntq6j.jpg)

Figure 8: Finding the repo URL.

At this point, you would ordinarily follow the instructions at GitHub by pushing up the default `master` branch, but [recall](https://www.learnenough.com/git-tutorial#sec-a_checkout_alias) that GitHub Pages uses the special `gh-pages` branch ([Box 3](https://www.learnenough.com/html-tutorial#aside-github_pages)) in place of `master`. As a result, before proceeding we’ll create the `gh-pages`branch using the `-b` option to `git checkout`[7](https://www.learnenough.com/html-tutorial#cha-0_footnote-7) and then push it to GitHub:

```
$ git checkout -b gh-pages
$ git push -u origin gh-pages

```

The result should appear as in [Figure 9](https://www.learnenough.com/html-tutorial#fig-repo_page). Use your technical sophistication ([Box 1](https://www.learnenough.com/html-tutorial#aside-technical_sophistication)) if any of your results don’t match the ones shown.

![images/figures/repo_page](https://ws4.sinaimg.cn/large/006tNc79gy1fm65dwezjmj30vi0ntq6j.jpg)

Figure 9: The initial repo page at GitHub.

As noted in [Box 3](https://www.learnenough.com/html-tutorial#aside-github_pages), our sample website is already live on the Web via GitHub pages. Its location is given by a github.io URL based on the username and repo name ([Listing 3](https://www.learnenough.com/html-tutorial#code-github_pages_url)).

Listing 3: The template for a GitHub Pages URL.

```
https://<username>.github.io/<repo_name>

```

For example, the Learn Enough version of the sample website lives at the URL <http://learnenough.github.io/sample_website>.

If you visit your version of this site, it should resolve properly, and it should even automatically serve up the contents of `index.html`. Because those contents are empty, though, the current appearance is a little underwhelming ([Figure 10](https://www.learnenough.com/html-tutorial#fig-empty_website)). We’ll take our first steps toward changing this sad state of affairs in [Section 1.3](https://www.learnenough.com/html-tutorial#sec-first_tag), and then we’ll [knock it up a notch](https://youtu.be/o4BOZcDMw_A) starting in [Section 2](https://www.learnenough.com/html-tutorial#sec-filling_in_the_index_page).

![images/figures/empty_website](https://ws3.sinaimg.cn/large/006tNc79gy1fm65dzg10lj30vk0ntab0.jpg)

Figure 10: The current underwhelming appearance of our live website.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_project_start)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. [Figure 9](https://www.learnenough.com/html-tutorial#fig-repo_page) shows a section for a README file about the project. Add and commit a file called `README.md`, taking care to use at least a few [Markdown](https://daringfireball.net/projects/markdown/) tags. What is the result at GitHub?
2. What happens if you visit `<username>.github.io/<repo_name>/README.md`in a browser? What does this imply about including sensitive information in a public website repo?

### [1.3The first tag](https://www.learnenough.com/html-tutorial#sec-first_tag)

In order to initialize the Git repository in [Section 1.2](https://www.learnenough.com/html-tutorial#sec-project_start), we needed only an empty `index.html` file, but of course our sample site will eventually have much more than that. In this section, we’ll begin by adding some content in a single tag—just enough to give us a site to view, commit, and deploy. That’s a huge accomplishment, though, and will serve as an essential foundation for what follows.

Now that an empty index page has been created, you should open `index.html` using your favorite editor, which for the purposes of this tutorial we’ll assume is Atom. It’s possible to open the file directly using `File > Open`, but (as [noted](https://www.learnenough.com/text-editor-tutorial#sec-editing_projects) in [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial)) these days all the cool kids open the full HTML project directly at the command line ([Figure 11](https://www.learnenough.com/html-tutorial#fig-cool_kids)):[8](https://www.learnenough.com/html-tutorial#cha-0_footnote-8)

```
$ atom .

```

([Recall](https://www.learnenough.com/command-line-tutorial#sec-navigating_directories) from [*Learn Enough Command Line to Be Dangerous*](http://learnenough.com/command-line-tutorial) that `.` (“dot”) refers to the current directory.)

![images/figures/cool_kids](https://ws4.sinaimg.cn/large/006tNc79gy1fm65e4ni10j30hs0bogqo.jpg)

Figure 11: All the cool kids open HTML projects directly at the command line.

Even though we have only one file for now (and possibly a README ([Section 1.2.1](https://www.learnenough.com/html-tutorial#sec-exercises_project_start))), opening the full project is a good habit to cultivate, since it allows us to easily open and edit multiple files in the same project. We’ll put this technique to good use when we start making additional pages in [Section 3.1](https://www.learnenough.com/html-tutorial#sec-an_html_page_about_html).

At this point, we’re ready to fill the index file with some content, which should consist of the phrase “Hello, world!” ([Listing 4](https://www.learnenough.com/html-tutorial#code-hello_world)) enclosed in the *paragraph tag* `p`. Note that the `p`tag has exactly the same form as the `strong` tag ([Figure 5](https://www.learnenough.com/html-tutorial#fig-anatomy_of_a_tag)).

Listing 4: A short paragraph with the contents “Hello, world!”.`index.html`

```
<p>Hello, world!</p>

```

We see in [Figure 12](https://www.learnenough.com/html-tutorial#fig-hello_world_in_editor) that Atom automatically highlights the HTML source, which it knows to do because of the `.html` extension on the filename. This *syntax highlighting* is irrelevant to the computer—in fact, it takes place purely in the editor and doesn’t have anything to do with `index.html` itself—but it makes it easier for humans to distinguish the difference between tags and content. (This is also why we use syntax highlighting in this tutorial’s code listings.)

![images/figures/hello_world_in_editor](https://ws4.sinaimg.cn/large/006tNc79gy1fm65e8xmjcj30m30ntdgy.jpg)

Figure 12: “Hello, world!” in a text editor.

Having made a change to add content to `index.html`, let’s view the result in a browser.On macOS, you can do this using the `open` command:

```
$ open index.html    # macOS only

```

On many Linux systems, you can use the similar `xdg-open` command:

```
$ xdg-open index.html    # Linux only

```

A technique that works on almost any system is to view the `sample_website` directory in graphical file browser and double-click the filename ([Figure 13](https://www.learnenough.com/html-tutorial#fig-graphical_browser_index)).

![images/figures/graphical_browser_index](https://ws1.sinaimg.cn/large/006tNc79gy1fm65eed70hj30oi0f8jta.jpg)

Figure 13: Double-clicking `index.html` should open it in the default browser.

No matter how you do it, the result should be to open `index.html` in the default browser on your system, which should appear something like [Figure 14](https://www.learnenough.com/html-tutorial#fig-hello_world_local_browser).

![images/figures/hello_world_local_browser](https://ws4.sinaimg.cn/large/006tNc79gy1fm65eixaz2j30vk0ntgmp.jpg)

Figure 14: The index page in a local browser.

Note that the “URL” in this [Figure 14](https://www.learnenough.com/html-tutorial#fig-hello_world_local_browser) will be a *local* file, like this:

```
file:///Users/mhartl/repos/sample_website/index.html

```

This is because the index page is on our local system, and hasn’t yet been deployed to the live Web.

We know how to remedy this, though—commit our changes to the local Git repository and push up to GitHub Pages:

```
$ git commit -am "Add a short paragraph"
$ git push

```

Upon refreshing the browser pointed at the sample website’s GitHub Pages URL ([Listing 3](https://www.learnenough.com/html-tutorial#code-github_pages_url)), the result should look something like [Figure 15](https://www.learnenough.com/html-tutorial#fig-hello_world_live_browser). (You may have to wait a few moments for GitHub Pages to load your site. This happens only the first time, and on subsequent requests the response will be lightning-fast.)

![images/figures/hello_world_live_browser](https://ws4.sinaimg.cn/large/006tNc79gy1fm65eo4dzij30vk0ntgmp.jpg)

Figure 15: The index page on the live Web.

Although the appearance is identical to the local version in [Figure 14](https://www.learnenough.com/html-tutorial#fig-hello_world_local_browser), by inspecting the address bar you should be able to confirm that the URL is at github.io, which means that the page is now available on the live Web.

Congratulations! You’ve just published a production website.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_first_tag)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Replace the contents of `index.html` with the markup from [Listing 2](https://www.learnenough.com/html-tutorial#code-exercise_snippet). Can you guess what the `a` tag does?
2. Use your browser’s *web inspector* to inspect the source from the previous exercise. (Google for “<browser> web inspector” to learn how to use your browser’s web inspector. Or just right-click.) Does it differ in any way from [Listing 2](https://www.learnenough.com/html-tutorial#code-exercise_snippet)?

### [1.4An HTML skeleton](https://www.learnenough.com/html-tutorial#sec-an_html_skeleton)

Although modern web browsers are highly [fault-tolerant](https://en.wikipedia.org/wiki/Fault_tolerance) and will render simple HTML like [Listing 4](https://www.learnenough.com/html-tutorial#code-hello_world) just fine, it’s dangerous to rely on this behavior. Indeed, we saw in [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial) that omitting a single tag resulted in the trademark character ™ not rendering properly. This is exactly the sort of thing that can go wrong when you don’t use a fully valid HTML page. To avoid these sorts of problems, from now on all of our sample web pages will use valid HTML to ensure that they will render properly in the broadest possible range of browsers.

![images/figures/about_page_broken](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ewkuklj30jg0eoabz.jpg)

Figure 16: The broken About page from [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial).

The prototypical HTML skeleton begins with an `html` tag containing two elements, a `head` and a `body`. These latter tags are *nested* inside the `html` tag, as follows:

```
<html><head></head><body></body></html>

```

Because this is hard to read, it’s conventional to format the tags using spaces and newlines to make the structure more apparent at a glance:

```
<html>
  <head>
  </head>
  <body>
  </body>
</html>

```

Because HTML generally ignores extra space, it makes no difference in the appearance of the page, but this formatting makes it easier for us to understand the source of the document ([Box 4](https://www.learnenough.com/html-tutorial#aside-formatting_html)).

> Box 4. Formatting HTML
>
> In order to make HTML easier to read, it’s conventional to add extra spaces and newlines to make the document’s structure clear at a glance. It might look a little strange at first, but it’s a style convention in the development world that helps keep source code readable (and coders sane).
>
> Generally speaking, HTML ignores extra space when displaying in a browser, so
>
> ```
>   <p>Hello, world!</p>
> ```
>
> will look the same as
>
> ```
>   <p>Hello,
>                world!
>
>                </p>
> ```
>
> It’s a good practice to keep your HTML formatting tidy, and it’s clear that the former is easier to read.
>
> The readability of the markup can change with time, though, especially after the text grows to more than a couple of sentences, or when there are additional HTML elements nested inside. To keep our content straight and not lose track of tags, in these cases we’ll need to format the code more rigorously.
>
> There are no universal rules for formatting markup, but a good rule of thumb is to put new tags on their own line unless they fit easily on one, with lines inside those tags indented one level:
>
> ```
>   <p>Hello, world!</p>
>
>   <p>
>     Lorem ipsum dolor sit amet, consectetur
>     adipisicing elit, sed do eiusmod tempor
>     incididunt ut labore et dolore magna aliqua.
>     Ut enim ad minim veniam
>   </p>
> ```
>
> The main exception to the new-line rule involves tags that modify text in a paragraph. For instance, most people do not add line breaks or indentation for elements that are inside lines of text (referred to as *inline elements*) like the `<strong>make them strong</strong>` example from [Listing 1](https://www.learnenough.com/html-tutorial#code-first_example). We’ll talk more about these types of inline elements, and how they differ from so-called *block elements*, in [Section 3.2](https://www.learnenough.com/html-tutorial#sec-tables).
>
> What constitutes an indentation “level” varies by developer, but we prefer the two-space convention shown above. Four spaces are also common, but in our experience this sends the content running off the right side of the page a little too fast. Some developers use tabs instead of spaces, but (at the risk of starting a [holy war](http://catb.org/jargon/html/H/holy-wars.html)) we think this should be strenuously avoided. The main issue is that the display of tab characters is device-dependent, so markup that looks great in a text editor could look terrible using `less` at the command line.
>
> It’s important to make sure your editor is configured properly to use spaces (sometimes confusingly called *emulated tabs*) instead of genuine tabs. Refer to [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial) or use your technical sophistication ([Box 1](https://www.learnenough.com/html-tutorial#aside-technical_sophistication)) to figure out how.
>
> Finally, it’s worth noting that many modern text editors include a way to format HTML automatically. For example, in Atom it’s `Edit > Lines > Auto Indent`. This can be a big help when indenting larger HTML files, especially if they come from an outside source and aren’t already nicely formatted.
>

The section of the HTML that is wrapped by `<head>` and `</head>` is a header container that defines *metadata*, a fancy word that just means data about data. This `<head>` section is not displayed to users in their browser window, and therefore gives developers the ability to tell the browser where to find other files (such as CSS and JavaScript) that will be used to properly display the page’s content, *without* having that information show up in the actual content of the web page. (We’ll cover more things that can be added to the HTML header starting in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial).)

Meanwhile, the content inside `<body>` and `</body>` is what gets displayed to the browser. Every website you’ve ever seen consists of content inside an HTML `body` tag.Once we’ve defined the contents of the `head` tag, most of the modifications we’ll make to the site will be inside the `body` tag.

To complete the skeleton, there are only two more required elements, one required and one optional but strongly recommended. First, we need to tell browsers what the *document type* is, and inside the `head` tag we need to define a nonempty `title`, as seen in [Listing 5](https://www.learnenough.com/html-tutorial#code-html_skeleton_almost_done).

Listing 5: A nearly complete HTML skeleton.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
  </body>
</html>

```

Here the `DOCTYPE` is an irregular tag, and you should not spend even a millisecond worrying about its exact form. (Why is there an exclamation point before `DOCTYPE`? We have no idea.) Meanwhile, the `title` tag has exactly the same form as the `p` tag we saw in [Section 1.3](https://www.learnenough.com/html-tutorial#sec-first_tag) (and the `strong` tag before that ([Figure 5](https://www.learnenough.com/html-tutorial#fig-anatomy_of_a_tag))).

As you can verify by using the W3C [HTML validator](https://validator.w3.org/), the page in [Listing 5](https://www.learnenough.com/html-tutorial#code-html_skeleton_almost_done) validates as HTML5 ([Figure 17](https://www.learnenough.com/html-tutorial#fig-valid_html_5)). (An empty `title` would be invalid, but an empty `body` is fine.)

![images/figures/valid_html_5](https://ws4.sinaimg.cn/large/006tNc79gy1fm65f2pb93j30d1061gm5.jpg)

Figure 17: The HTML in [Listing 5](https://www.learnenough.com/html-tutorial#code-html_skeleton_almost_done) is valid but incomplete.

On the other hand, we learned in [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial) ([Figure 16](https://www.learnenough.com/html-tutorial#fig-about_page_broken)) that we need one more thing: we need to tell the browser which *character set* to use so that it can handle the expanded range of characters (called [Unicode](https://en.wikipedia.org/wiki/Unicode)), which includes symbols like ™ and ©, accented characters (as in *voilà*), etc. We can do this by adding the `meta` tag to the `head`, as shown in [Listing 6](https://www.learnenough.com/html-tutorial#code-meta_charset).

Listing 6: Adding a `meta` tag to define the character set.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
    <meta charset="utf-8">
  </head>
  <body>
  </body>
</html>

```

By the way, the `meta` tag is a special kind of tag called a *void element*, and doesn’t have a closing tag. Because of this, void elements are also called *self-closing tags*.

With that, the skeleton is complete ([Figure 18](https://www.learnenough.com/html-tutorial#fig-skeleton)),[9](https://www.learnenough.com/html-tutorial#cha-0_footnote-9) and is listed again for reference in [Listing 7](https://www.learnenough.com/html-tutorial#code-html_skeleton).

![images/figures/html_skeleton](https://ws2.sinaimg.cn/large/006tNc79gy1fm65f97vsnj30hs0dcwos.jpg)

Figure 18: A complete HTML skeleton.

Listing 7: The skeleton for a basic HTML document.

```
1 <!DOCTYPE html>
2 <html>
3   <head>
4     <title>Page Title</title>
5     <meta charset="utf-8">
6   </head>
7   <body>
8   </body>
9 </html>

```

Because of the importance of this HTML skeleton, let’s review its elements line by line:

1. The doctype declaration
2. Opening `html` tag
3. Opening `head` tag
4. Opening and closing `title` tags (with the content of the page title)
5. The `meta` tag defining the character set
6. Closing `head` tag
7. Opening `body` tag
8. Closing `body` tag
9. Closing `html` tag

Combining the original paragraph from [Listing 4](https://www.learnenough.com/html-tutorial#code-hello_world) with the skeleton in [Listing 7](https://www.learnenough.com/html-tutorial#code-html_skeleton) gives us the code for the first valid HTML page in our sample website, as shown in [Listing 8](https://www.learnenough.com/html-tutorial#code-hello_world_complete).

Listing 8: A valid “Hello, world!” page.`index.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
    <meta charset="utf-8">
  </head>
  <body>
    <p>Hello, world!</p>
  </body>
</html>

```

Note in [Listing 8](https://www.learnenough.com/html-tutorial#code-hello_world_complete) that we’ve placed the paragraph from [Listing 4](https://www.learnenough.com/html-tutorial#code-hello_world) inside the `body` tag, as required by the HTML standard.

After refreshing the browser, the result of [Listing 8](https://www.learnenough.com/html-tutorial#code-hello_world_complete) is virtually the same as we saw in [Figure 15](https://www.learnenough.com/html-tutorial#fig-hello_world_live_browser). The only visible difference in the body of the page is a small amount of additional space around the paragraph, as shown in [Figure 19](https://www.learnenough.com/html-tutorial#fig-valid_hello_world).

![images/figures/valid_hello_world](https://ws2.sinaimg.cn/large/006tNc79gy1fm65fd12igj30vk0ntdgx.jpg)

Figure 19: A valid “Hello, world!” page.

A second, browser-dependent difference involves the page title, which some browsers display in the default tab ([Figure 20](https://www.learnenough.com/html-tutorial#fig-page_title_chrome)), and others don’t show unless you have a second tab in addition to the first ([Figure 21](https://www.learnenough.com/html-tutorial#fig-page_title_safari)). In any case, the page title is needed even if it’s not displayed, as it’s required by the HTML standard, and is important for screen readers and the web spiders used by search engines to index the Web.

![images/figures/page_title_chrome](https://ws2.sinaimg.cn/large/006tNc79gy1fm65fgb5oij30vk0ntdht.jpg)

Figure 20: The page title in Chrome.

![images/figures/page_title_safari](https://ws4.sinaimg.cn/large/006tNc79gy1fm65fisdknj30hs0dcwos.jpg)

Figure 21: The page title in Safari.

With that, we’re ready to commit our changes and push the results to GitHub Pages:

```
$ git commit -am "Convert index page to fully valid HTML"
$ git push

```

The result appears in [Figure 22](https://www.learnenough.com/html-tutorial#fig-valid_hello_world_production).

![images/figures/valid_hello_world_production](https://ws3.sinaimg.cn/large/006tNc79gy1fm65fpt4ymj30vj0ntgmm.jpg)

Figure 22: The valid “Hello, world!” page in production.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_an_html_skeleton)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Using the [HTML validator](https://validator.w3.org/), confirm that [Listing 6](https://www.learnenough.com/html-tutorial#code-meta_charset) is valid HTML.
2. Remove `</title>` from [Listing 9](https://www.learnenough.com/html-tutorial#code-html_closing_tags) and verify that it breaks the page ([Figure 23](https://www.learnenough.com/html-tutorial#fig-close_tags)).This underscores the importance of closing your tags. Confirm using the HTML validator that the resulting code fails validation.
3. By pasting in the contents of [Listing 10](https://www.learnenough.com/html-tutorial#code-address) into `index.html`, confirm that the browser ignores the extra whitespace (including newlines) in the mailing address shown in [Listing 10](https://www.learnenough.com/html-tutorial#code-address).
4. By adding the break tag `<br>` to the end of each of the first two lines of the address, obtain the nicely formatted address shown in [Figure 24](https://www.learnenough.com/html-tutorial#fig-formatted_address).

Listing 9: The index page with a missing closing tag.`index.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title
    <meta charset="utf-8">
  </head>
  <body>
  </body>
</html>

```

![images/figures/close_tags](https://ws1.sinaimg.cn/large/006tNc79gy1fm65fw9896j30vk0ntdgv.jpg)

Figure 23: The look of failure… Close your tags!

Listing 10: An unformatted address.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Who am I?</title>
    <meta charset="utf-8">
  </head>
  <body>
    Jean Valjean
    55 Rue Plumet
    Amonate, VA 24601
  </body>
</html>

```

![images/figures/formatted_address](https://ws3.sinaimg.cn/large/006tNc79gy1fm65g7d1psj30vj0ntab9.jpg)

Figure 24: A nicely formatted address.

## [2Filling in the index page](https://www.learnenough.com/html-tutorial#sec-filling_in_the_index_page)

Now that we’ve created and deployed a valid HTML page, it’s time to start filling in the sample website. We’ll begin by scoping out the structure of our index page while adding a more normal-sized paragraph ([Section 2.1](https://www.learnenough.com/html-tutorial#sec-headings)). We’ll then format the resulting text ([Section 2.2](https://www.learnenough.com/html-tutorial#sec-text_formatting)) while adding links ([Section 2.3](https://www.learnenough.com/html-tutorial#sec-links)) and images ([Section 2.4](https://www.learnenough.com/html-tutorial#sec-images)). Starting in [Section 3](https://www.learnenough.com/html-tutorial#sec-more_pages), we’ll add two more pages to go along with our index page, introducing several more important HTML tags along the way.

### [2.1Headings](https://www.learnenough.com/html-tutorial#sec-headings)

As noted in [Section 1.2](https://www.learnenough.com/html-tutorial#sec-project_start), our main index page will include some information about Learn Enough to Be Dangerous, so we’ll start by updating the `title` tag contents with a new title, as shown in [Listing 11](https://www.learnenough.com/html-tutorial#code-new_title).

Listing 11: Adding a new title.`index.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>Learn Enough to Be Dangerous</title>
    <meta charset="utf-8">
  </head>
  <body>
    <p>Hello, world!</p>
  </body>
</html>

```

Next, we’ll replace the paragraph in the HTML `body` with several *headings*, constituting an outline of our document. The results appear in [Listing 12](https://www.learnenough.com/html-tutorial#code-headings).

Listing 12: Scoping out our index page with headings.`index.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>Learn Enough to Be Dangerous</title>
    <meta charset="utf-8">
  </head>
  <body>

    <h1>The Learn Enough Story</h1>

    <h2>Background</h2>

    <h2>Founders</h2>

    <h3>Michael Hartl</h3>

    <h3>Lee Donahoe</h3>

    <h3>Nick Merwin</h3>

  </body>
</html>

```

[Listing 12](https://www.learnenough.com/html-tutorial#code-headings) shows how to use the HTML header tags `h1`, `h2`, and `h3`, which represent three levels of headings. In this case, the top-level `h1` heading contains the main subject of the page:

```
<h1>The Learn Enough Story</h1>

```

The next two headings indicate additional subjects—in this case, some background on the company and some details about the founders:

```
<h2>Background</h2>

<h2>Founders</h2>

```

Because these subjects are subsidiary to the main story, they use the second-level heading `h2`. Finally, [Listing 12](https://www.learnenough.com/html-tutorial#code-headings) uses the third-level heading `h3` to list the three Learn Enough founders:

```
<h3>Michael Hartl</h3>

<h3>Lee Donahoe</h3>

<h3>Nick Merwin</h3>

```

As you might guess, most browsers render the top-level `h1` heading in a large font size, with `h2` and `h3` getting progressively smaller. (Figuring out how many heading sizes HTML supports is left as an exercise ([Section 2.1.1](https://www.learnenough.com/html-tutorial#sec-exercises_headings)).) The result appears in [Figure 25](https://www.learnenough.com/html-tutorial#fig-headings).

![images/figures/headings](https://ws1.sinaimg.cn/large/006tNc79gy1fm65gh0huyj30vj0ntjsz.jpg)

Figure 25: The initial headings for the index page.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_headings)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. [Listing 12](https://www.learnenough.com/html-tutorial#code-headings) uses headings `h1` down to `h3`. By experimenting directly in `index.html`, determine how many levels of headings HTML supports.

### [2.2Text formatting](https://www.learnenough.com/html-tutorial#sec-text_formatting)

Having added the headings to block out the structure of our document, let’s now add an introductory paragraph describing the subject of the page. Unlike our previous one-line paragraph ([Listing 4](https://www.learnenough.com/html-tutorial#code-hello_world)), this paragraph will include several lines, as well as requiring some text formatting (this section) and a link ([Section 2.3](https://www.learnenough.com/html-tutorial#sec-links)).

The paragraph itself appears in [Listing 13](https://www.learnenough.com/html-tutorial#code-paragraph), where the vertical dots indicate omitted content (just so we don’t have to include all the tags in every code listing).

Listing 13: Adding a paragraph.`index.html`

```
    .
    .
    .
    <h1>The Learn Enough Story</h1>

    <p>
      Learn Enough to Be Dangerous is a leader in the movement to teach
      technical sophistication, the seemingly magical ability to take
      command of your computer and get it to do your bidding. This includes
      everything from command lines and coding to guessing keyboard shortcuts,
      Googling error messages, and knowing when to just reboot the darn thing.
      We believe there are at least a billion people who can benefit from
      learning technical sophistication, probably more. To join our
      movement, sign up for our official email list now.
    </p>
    .
    .
    .

```

Note that the content is now indented inside the `p` tag:

```
<p>
  content
</p>

```

As discussed in [Box 4](https://www.learnenough.com/html-tutorial#aside-formatting_html), this makes the structure easier to see without affecting the appearance of the page.

It’s also worth noting that [Listing 13](https://www.learnenough.com/html-tutorial#code-paragraph) includes newlines at the end of each line, but this is mainly so that the paragraph contents fit within in the constraints of a book. As seen in [Figure 26](https://www.learnenough.com/html-tutorial#fig-paragraph), these newlines don’t have any effect on the display, and in real life it’s probably more common to have the content be all on one line, and simply enable word wrap (called “soft wrap” in Atom), as [described](http://www.learnenough.com/text-editor-tutorial#sec-opening) in [*Learn Enough Text Editor to Be Dangerous*](http://learnenough.com/text-editor-tutorial). This is what we recommend you do if you type the contents of [Listing 13](https://www.learnenough.com/html-tutorial#code-paragraph) in by hand.

![images/figures/paragraph](https://ws1.sinaimg.cn/large/006tNc79gy1fm65h4kdztj30vj0nttbf.jpg)

Figure 26: Adding a paragraph.

#### [Emphasized text](https://www.learnenough.com/html-tutorial#sec-emphasized_text)

The paragraph in [Listing 13](https://www.learnenough.com/html-tutorial#code-paragraph) has the right content, but it also introduces the new term *technical sophistication*, and it’s a common typesetting convention to *emphasize* such terms using italics. As mentioned briefly in [Box 2](https://www.learnenough.com/html-tutorial#aside-semantic_tale), we can accomplish this using the `em`tag, like this:

```
<em>technical sophistication</em>

```

Applying this idea to [Listing 13](https://www.learnenough.com/html-tutorial#code-paragraph) gives the result shown in [Listing 14](https://www.learnenough.com/html-tutorial#code-em_tag).

Listing 14: Emphasized text.`index.html`

```
    .
    .
    .
    <h1>The Learn Enough Story</h1>

    <p>
      Learn Enough to Be Dangerous is a leader in the movement to teach
      <em>technical sophistication</em>, the seemingly magical ability to take
      command of your computer and get it to do your bidding. This includes
      everything from command lines and coding to guessing keyboard shortcuts,
      Googling error messages, and knowing when to just reboot the darn thing.
      We believe there are at least a billion people who can benefit from
      learning technical sophistication, probably more. To join our
      movement, sign up for our official email list now.
    </p>
    .
    .
    .

```

We can confirm that this worked by refreshing the browser, which shows that *technical sophistication* is properly emphasized ([Figure 27](https://www.learnenough.com/html-tutorial#fig-emphasized_text)).

![images/figures/emphasized_text](https://ws1.sinaimg.cn/large/006tNc79gy1fm65hgwa44j30vj0ntju5.jpg)

Figure 27: Emphasized text.

#### [Strong text](https://www.learnenough.com/html-tutorial#sec-strong_tag)

As we saw briefly in [Section 1.1](https://www.learnenough.com/html-tutorial#sec-html_tags), another possibility for drawing attention to particular text is to make it **strong** using the `strong` tag, which most browsers render as boldface text. In this case, we’d like to indicate the strength of our belief that **at least a billion people** can potentially benefit from learning technical sophistication, which we can do like this:

```
<strong>at least a billion people</strong>

```

Applying this idea to [Listing 14](https://www.learnenough.com/html-tutorial#code-em_tag) gives [Listing 15](https://www.learnenough.com/html-tutorial#code-strong_tag).

Listing 15: Strong text.`index.html`

```
    .
    .
    .
    <p>
      Learn Enough to Be Dangerous is a leader in the movement to teach
      <em>technical sophistication</em>, the seemingly magical ability to take
      command of your computer and get it to do your bidding. This includes
      everything from command lines and coding to guessing keyboard shortcuts,
      Googling error messages, and knowing when to just reboot the darn thing.
      We believe there are <strong>at least a billion people</strong> who
      can benefit from learning technical sophistication, probably more. To
      join our movement, sign up for our official email list now.
    </p>
    .
    .
    .

```

Refreshing the browser confirms that the text is now set in bold ([Figure 28](https://www.learnenough.com/html-tutorial#fig-strong)).

![images/figures/strong](https://ws4.sinaimg.cn/large/006tNc79gy1fm65hqqx88j30vj0ntwhb.jpg)

Figure 28: Strong text.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_text_formatting)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Add the paragraph shown in [Listing 16](https://www.learnenough.com/html-tutorial#code-strong_founders_paragraph) under **founders**, then make the text **at least a billion people** bold ([Figure 29](https://www.learnenough.com/html-tutorial#fig-strong_founders_paragraph)).
2. What happens if you nest the `em` and `strong` tags? Is is possible to make something both italic ****\*and***** bold?

Listing 16: A paragraph with something to be made stronger.`index.html`

```
    .
    .
    .
    <h3>Founders</h3>

    <p>
      Learn Enough to Be Dangerous was founded in 2015 by Michael Hartl, Lee
      Donahoe, and Nick Merwin. We believe that the kind of technical
      sophistication taught by the Learn Enough tutorials can benefit
      at least a billion people, and probably more.
    </p>
    .
    .
    .

```

![images/figures/strong_founders_paragraph](https://ws1.sinaimg.cn/large/006tNc79gy1fm65hy1imcj30vj0ntq6f.jpg)

Figure 29: The appearance of a properly modified [Listing 16](https://www.learnenough.com/html-tutorial#code-strong_founders_paragraph).

### [2.3Links](https://www.learnenough.com/html-tutorial#sec-links)

As mentioned in [Section 1.1](https://www.learnenough.com/html-tutorial#sec-html_tags), much of the point of the Web is hypertext, with hyperlinks that let us move from one page to the next. The way to make such hyperlinks (or *links* for short) is with the HTML anchor tag `a`. (Why isn’t it called `link`? We don’t know, but at least `a` is short.)

In reading the paragraph from [Listing 13](https://www.learnenough.com/html-tutorial#code-paragraph), you may have noticed that the line

```
sign up for our official email list now

```

is practically begging for a link to a place where people can actually sign up for the email list. The exact text to use for the link is the subject of some debate, with some holding that links should be nouns, with others preferring to link a [call to action](https://en.wikipedia.org/wiki/Call_to_action_(marketing)) if possible. We take a pragmatic approach, linking based on what seems most natural. In this case, we’ll go with linking the text “sign up for our official email list”, like this:

```
<a href="http://learnenough.com/email">sign up for our official email list</a>

```

This contains our first example of an *attribute*, which is a bit of text inside an HTML tag that supplies extra information about how to process it. In this case, the attribute is `href`, for “hypertext reference”, and the value is the URL for the Learn Enough email list signup form.

Adding the email list link to the paragraph from [Listing 15](https://www.learnenough.com/html-tutorial#code-strong_tag) gives [Listing 17](https://www.learnenough.com/html-tutorial#code-anchor_tag). Note how the text of the link breaks across two lines (something we saw before in [Listing 1](https://www.learnenough.com/html-tutorial#code-first_example)). Because HTML is insensitive to whitespace, this is effectively the same as having it all on one line.

Listing 17: Adding a link.

```
    .
    .
    .
    <p>
      Learn Enough to Be Dangerous is a leader in the movement to teach <em>
      technical sophistication</em>, the seemingly magical ability to take
      command of your computer and get it to do your bidding. This includes
      everything from command lines and coding to guessing keyboard shortcuts,
      Googling error messages, and knowing when to just reboot the darn thing.
      We believe there are <strong>at least a billion people</strong> who
      can benefit from learning technical sophistication, probably more. To
      join our movement, <a href="http://learnenough.com/email">sign
      up for our official email list</a> now.
    </p>
    .
    .
    .

```

The result of [Listing 17](https://www.learnenough.com/html-tutorial#code-anchor_tag) appears in [Figure 30](https://www.learnenough.com/html-tutorial#fig-anchor_tag).

![images/figures/anchor_tag](https://ws1.sinaimg.cn/large/006tNc79gy1fm65i2l9oaj30vj0ntdjc.jpg)

Figure 30: The result of adding a link.

Now that we know how to make links, we’re ready to add a paragraph on the background of Learn Enough to Be Dangerous, which is both rich with links and includes further examples of the text-formatting tags shown in [Section 2.2](https://www.learnenough.com/html-tutorial#sec-text_formatting). The resulting paragraph, shown in [Listing 18](https://www.learnenough.com/html-tutorial#code-examples_paragraph), should be placed under the second-level heading from [Listing 12](https://www.learnenough.com/html-tutorial#code-headings).Because it contains so many good examples of the tags we’ve covered so far, we recommend you type it in by hand.

Listing 18: Adding a paragraph using several useful tags.

```
    .
    .
    .
    <h2>Background</h2>

    <p>
      Learn Enough to Be Dangerous is an outgrowth of the
      <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a> and the
      <a href="http://www.softcover.io/">Softcover publishing platform</a>.
      This page is part of the sample site for
      <a href="http://learnenough.com/html-tutorial"><em>Learn Enough HTML to
      Be Dangerous</em></a>, which teaches the basics of
      <strong>H</strong>yper<strong>T</strong>ext <strong>M</strong>arkup
      <strong>L</strong>anguage, the universal language of the World Wide Web.
      Other related tutorials can be found at
      <a href="http://learnenough.com/">learnenough.com</a>.
    </p>
    .
    .
    .

```

It’s worth noting that [Listing 18](https://www.learnenough.com/html-tutorial#code-examples_paragraph) contains an example of tag nesting, in the form of the link to the present tutorial:

```
<a href="..."><em>Learn Enough HTML to Be Dangerous</em></a>

```

As you might expect, this produces a link to emphasized text, as shown in [Figure 31](https://www.learnenough.com/html-tutorial#fig-examples_paragraph). You might also note that some of the links in [Figure 31](https://www.learnenough.com/html-tutorial#fig-examples_paragraph) are a different color, which is an indication that the links have been followed. (This is the default behavior for link colors, but it can be overridden by CSS, as discussed in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial) and mentioned briefly in [Section 4.6.1](https://www.learnenough.com/html-tutorial#sec-exercises_navigation_styling).)

![images/figures/examples_paragraph](https://ws2.sinaimg.cn/large/006tNc79gy1fm65i6zllwj30vj0ntn1m.jpg)

Figure 31: Adding a paragraph with formatting and links.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_links)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Using the content shown in [Listing 19](https://www.learnenough.com/html-tutorial#code-founder_bios), add short founder bios to the index page.
2. Now add Twitter follow links as shown in [Listing 20](https://www.learnenough.com/html-tutorial#code-twitter_links). Does the content appear as shown in [Figure 32](https://www.learnenough.com/html-tutorial#fig-exercises_links)?
3. It’s sometimes convenient for external links (like those in the previous exercise) to open in a new browser tab. To do this, add the attribute `target="_blank"` to each of the Twitter links from [Listing 20](https://www.learnenough.com/html-tutorial#code-twitter_links). Does clicking on one of the links open in a new tab, as shown in [Figure 32](https://www.learnenough.com/html-tutorial#fig-exercises_links)?

Listing 19: Adding short founder biographies.`index.html`

```
    .
    .
    .
    <h2>Founders</h2>
    .
    .
    .
    <h3>Michael Hartl</h3>

    <p>
      Michael is the creator of the <a href="http://railstutorial.org/">
      Ruby on Rails Tutorial</a> and principal author of the
      <a href="http://learnenough.com/">Learn Enough to Be Dangerous</a>
      introductory sequence. He is an advanced student of
      <a href="http://kravmaga.com/">Krav Maga</a> and has a three-step
      plan for world domination. Rumors that he's secretly a supervillain
      are slightly exaggerated.
    </p>

    <h3>Lee Donahoe</h3>

    <p>
      When he's not literally swimming with sharks or hunting powder stashes
      on his snowboard, you can find Lee in front of his computer designing
      interfaces, doing front-end development, or writing some of the
      interface-related Learn Enough tutorials.
    </p>

    <h3>Nick Merwin</h3>

    <p>
      You may have seen him shredding guitar live with Capital Cities on Jimmy
      Kimmel, Conan, or The Ellen Show, but rest assured Nick is a true nerd
      at heart. He's just as happy shredding well-spec'd lines of code from a
      tour bus as he is from his kitchen table.
    </p>
    .
    .
    .

```

Listing 20: Adding Twitter links to the bios.`index.html`

```
    .
    .
    .
    <h3>Michael Hartl</h3>
    .
    .
    .
    <p>
      You should follow Michael on Twitter
      <a href="http://twitter.com/mhartl">here</a>.
    </p>

    <h3>Lee Donahoe</h3>
    .
    .
    .
    <p>
      You should follow Lee on Twitter
      <a href="https://twitter.com/leedonahoe">here</a>.
    </p>

    <h3>Nick Merwin</h3>
    .
    .
    .
    <p>
      You should follow Nick on Twitter
      <a href="https://twitter.com/nickmerwin">here</a>.
    </p>

```

![images/figures/exercises_links](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ibj84zj30vj0nt10z.jpg)

Figure 32: The index page after the completion of the exercises.

### [2.4Adding images](https://www.learnenough.com/html-tutorial#sec-images)

At this point, our index page is coming into shape, but it’s still missing a critical feature: what would a website be without images (of cats!)? Fortunately, adding images is similar to adding links, although there is an important difference in the structure of the tags.Recall from [Section 2.3](https://www.learnenough.com/html-tutorial#sec-links) that anchor tags take the form

```
<a href="http://example.com/">Example site</a>

```

We can include images in a similar way using the `img` tag, with a source attribute `src`and an alternate attribute `alt`:

```
<img src="images/kitten.jpg" alt="An adorable kitten">

```

Here `src` has a path to the image (either on the filesystem or on the Web), while `alt`lets developers add a bit of alternate text that describes the image in words. On some browsers, this text will display if the user’s browser has a problem loading the image, but more importantly it will be read aloud (or even presented as braille) by screen readers used by the visually impaired, and is required by the HTML standard.[10](https://www.learnenough.com/html-tutorial#cha-0_footnote-10)

The important difference mentioned above is that the `img` tag *doesn’t* look like a typical tag, with content inside open and closing tags ([Figure 5](https://www.learnenough.com/html-tutorial#fig-anatomy_of_a_tag)). If it did, it would look like this:

```
<img src="…" alt="…">content</img>

```

Instead, the `img` tag has no content and no closing tag:

```
<img src="…" alt="…">

```

That final `>` is all that’s needed to close an `img` tag—like the `meta` tag discussed in [Section 1.4](https://www.learnenough.com/html-tutorial#sec-an_html_skeleton), `img` is a void element (self-closing tag). A second variant uses `/>` at the end, like this:

```
<img src="…" alt="…" />

```

This syntax is designed to conform to [XML](https://en.wikipedia.org/wiki/XML), a markup language related to HTML, but using `/>` is not required in HTML5. We mention it mainly because you will still sometimes run across the XML-style syntax in other people’s markup, and it’s important to know that the two styles are exactly equivalent.

Because the World Wide Web was apparently invented to share pictures of furry felines, we’ll add an image of an adorable kitten to our sample index page, as shown in ([Figure 33](https://www.learnenough.com/html-tutorial#fig-kitten)).[11](https://www.learnenough.com/html-tutorial#cha-0_footnote-11)

![images/figures/kitten](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ig6jtfj30hs0bt0wa.jpg)

Figure 33: The likely inspiration for the creation of the World Wide Web.

In order to link the kitten image, we could link directly to the source of [Figure 33](https://www.learnenough.com/html-tutorial#fig-kitten) from the live Web, like this:

```
<img src="http://example.com/images/kitten.jpg" alt="An adorable kitten">

```

This practice, called *hotlinking*, is generally considered bad form, for reasons we’ll explain in [Section 2.4.1](https://www.learnenough.com/html-tutorial#sec-hotlinking). Instead, we’ll copy the image to the local computer, which will then be uploaded automatically when we deploy to GitHub pages.

To do this, first create a directory called `images`:

```
$ mkdir images

```

Creating a separate `images` directory isn’t strictly necessary, but it’s useful for keeping our main project directory tidy. Next, download the image to the local disk using `curl`:[12](https://www.learnenough.com/html-tutorial#cha-0_footnote-12)

```
$ curl -o images/kitten.jpg -OL cdn.learnenough.com/kitten.jpg

```

Once the image is available on our local disk, we can use its location as the value of the `src` attribute. Because the image is part of the same web project as `index.html`, we can use the *relative path* to the image, like this:

```
<img src="images/kitten.jpg" alt="An adorable kitten">

```

The `src` attribute `images/kitten.jpg` will automatically be interpreted as the correct full path to the file, which locally might be

```
file:///Users/mhartl/repos/sample_website/images/kitten.jpg

```

and on the server will be something like

```
https://learnenough.github.io/sample_website/images/kitten.jpg

```

While we’re at it, we’ll add a paragraph giving some context about the creation of the World Wide Web (including a correction to the wildly inaccurate claims of its feline origins). The result appears in [Listing 21](https://www.learnenough.com/html-tutorial#code-web_developer_kitten).

Listing 21: An image, with a paragraph about the original web developer.`index.html`

```
    <h1>The Learn Enough Story</h1>
    .
    .
    .
    <p>
      HTML was created by the original "web developer", computer scientist
      <a href="https://en.wikipedia.org/wiki/Tim_Berners-Lee">Tim
      Berners-Lee</a>. It's not true that Sir Tim invented HTML in order to
      share pictures of his cat, but it would be cool if it were.
    </p>

    <img src="images/kitten.jpg" alt="An adorable kitten">

    <h2>Background</h2>
    .
    .
    .

```

After adding the contents of [Listing 21](https://www.learnenough.com/html-tutorial#code-web_developer_kitten) to `index.html`, the sample index page should look something like [Figure 34](https://www.learnenough.com/html-tutorial#fig-web_developer_kitten).

![images/figures/web_developer_kitten](https://ws3.sinaimg.cn/large/006tNc79gy1fm65izwowqj30vj0nth3t.jpg)

Figure 34: An awww-bligatory kitten image.

#### [Hotlinking](https://www.learnenough.com/html-tutorial#sec-hotlinking)

We mentioned above that it’s possible to link directly to images on the Web, a practice called *hotlinking*. The way to do this is to use a fully qualified URL as the `src`parameter, like this:

```
<img src="http://example.com/images/example.jpg" alt="A nonexistent example">

```

Hotlinking isn’t usually a good practice, mainly because the image has to be at that exact spot on that exact site or it will not load, putting you at the mercy of the site’s maintainer. The person who runs the site can also be charged for the bandwidth used to serve the image, so hotlinking is considered inconsiderate as well. For these reasons, we generally recommend using local images for most applications.[13](https://www.learnenough.com/html-tutorial#cha-0_footnote-13)

There are some important exceptions to the hotlinking rule, though, including an application known as *Gravatar*, which stands for “globally recognized avatar”. Gravatar allows you to associate standard images with particular email addresses, and is used to display profile pictures on a large variety of websites, including GitHub and WordPress.[14](https://www.learnenough.com/html-tutorial#cha-0_footnote-14) Gravatar images are specifically designed for hotlinking, so in this case the practice is actually encouraged. The image could still change, but in this case [it’s not a bug, it’s a feature](https://www.learnenough.com/command-line-tutorial#aside-speak_geek), because it gives the user control over their preferred profile image—if they update their picture, the change will automatically propagate to every site using the right Gravatar URL.

Gravatar URLs include a long string of hexadecimal digits (base 16, meaning 0–9 and a–f), like this:

```
https://gravatar.com/avatar/ffda7d145b83c4b118f982401f962ca6

```

Here `ffda7d145b83c4b118f982401f962ca6` is a unique string based on the email address associated with the Gravatar.[15](https://www.learnenough.com/html-tutorial#cha-0_footnote-15) Gravatar URLs also support *query parameters*, which are additional pieces of information that come after the main URL, like `?s=150`:

```
https://gravatar.com/avatar/ffda7d145b83c4b118f982401f962ca6?s=150

```

Query parameters come after a question mark `?`, in this case `s=150`, which consists of a *key* `s` and a *value* `150`.[16](https://www.learnenough.com/html-tutorial#cha-0_footnote-16) As you might be able to guess, `s` stands for “size”, and in this case the query parameter `s=150` sets the Gravatar size to 150 pixels. (By design, Gravatars are square, so a single parameter specifies the size uniquely.)

Using our newfound Gravatar knowledge, let’s add avatar images to our index page under each of the Learn Enough to Be Dangerous founder bios (as added in [Listing 19](https://www.learnenough.com/html-tutorial#code-founder_bios) from the exercises in [Section 2.3.1](https://www.learnenough.com/html-tutorial#sec-exercises_links)). In a typical dynamic web application, such as that developed in the [Ruby on Rails Tutorial](http://railstutorial.org/), these URLs would be [calculated on the fly](https://www.railstutorial.org/book/sign_up#sec-a_gravatar_image) based on the users’ email addresses, but for convenience we’ll supply you with the proper URLs. The result appears in [Listing 22](https://www.learnenough.com/html-tutorial#code-gravatar_hotlinks). (We’ve removed the leading indentation in [Listing 22](https://www.learnenough.com/html-tutorial#code-gravatar_hotlinks) so that the URLs fit, but in your `index.html` we suggest you keep the indentation as before.)

Listing 22: Adding Gravatar hotlinks for the Learn Enough founders.

```
.
.
.
<h2>Founders</h2>
.
.
.
<h3>Michael Hartl</h3>

<img src="https://gravatar.com/avatar/ffda7d145b83c4b118f982401f962ca6?s=150"
     alt="Michael Hartl">
.
.
.

<h3>Lee Donahoe</h3>

<img src="https://gravatar.com/avatar/b65522a6f3a6899705d119d7aa232a6d?s=150"
     alt="Lee Donahoe">
.
.
.

<h3>Nick Merwin</h3>

<img src="https://gravatar.com/avatar/e2d6ce2ba5c1b6d674ae8ff2b3b45d23?s=150"
     alt="Nick Merwin">
.
.
.

```

The result of adding the contents of [Listing 22](https://www.learnenough.com/html-tutorial#code-gravatar_hotlinks) should look something like [Figure 35](https://www.learnenough.com/html-tutorial#fig-gravatar_hotlinks), although your page may not match exactly ([Section 2.4.2](https://www.learnenough.com/html-tutorial#sec-exercises_images)).

![images/figures/gravatar_hotlinks](https://ws4.sinaimg.cn/large/006tNc79gy1fm65j5gi7wj30vj0nt0z3.jpg)

Figure 35: Adding Gravatar images.

With that, our sample website’s index page has (nearly) taken its final form, so now is a good time to commit the changes and push to the live server at GitHub Pages:

```
$ git add -A
$ git commit -m "Add content and some images"
$ git push

```

The result should look something like [Figure 36](https://www.learnenough.com/html-tutorial#fig-live_index_page).

![images/figures/live_index_page](https://ws1.sinaimg.cn/large/006tNc79gy1fm65jfw2n5j30vj0nt7mf.jpg)

Figure 36: The sample index page on the live Web.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_images)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Why might the images shown in [Figure 35](https://www.learnenough.com/html-tutorial#fig-gravatar_hotlinks) not match your results exactly? *Hint*: It’s not a bug, it’s a feature.
2. The kitten image in [Figure 33](https://www.learnenough.com/html-tutorial#fig-kitten) is available under a [Creative Commons](https://creativecommons.org/) license that requires attribution. We’ll fulfill this requirement by linking the image on our page to the [original image’s URL](https://www.flickr.com/photos/deborah_s_perspective/14144861329), which involves nesting the `a` and `img` tags, as shown in [Listing 23](https://www.learnenough.com/html-tutorial#code-image_link). (Be sure to replace `FILL_IN` with the right URL.) How does this change the page’s (a) appearance and (b) behavior?
3. Under the first paragraph on `index.html`, let’s add a link to the [Learn Enough Twitter account](http://twitter.com/learnenough). First, download the Twitter logo as shown in [Listing 24](https://www.learnenough.com/html-tutorial#code-twitter_curl). Then, add a link to both the page and the logo image, as shown in [Listing 25](https://www.learnenough.com/html-tutorial#code-learn_enough_twitter). Be sure to replace `FILL_IN` with the right path to the image. Note that [Listing 25](https://www.learnenough.com/html-tutorial#code-learn_enough_twitter) introduces *inline styling*, which is the subject of [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles). *Extra credit*: Follow Learn Enough on Twitter [here](http://twitter.com/learnenough).

Listing 23: Linking an image.`index.html`

```
    <p>
      HTML was created by the original "web developer", computer scientist
      <a href="https://en.wikipedia.org/wiki/Tim_Berners-Lee">Tim
      Berners-Lee</a>. It's not true that Sir Tim invented HTML in order to
      share pictures of his cat, but it would be cool if it were.
    </p>

    <a href="FILL_IN">
      <img src="images/kitten.jpg" alt="An adorable kitten">
    </a>

```

Listing 24: Downloading the Twitter logo.

```
$ curl -o images/small_twitter_logo.png \
>      -OL cdn.learnenough.com/small_twitter_logo.png

```

Note that the backslash `\` should be typed, but your shell will include `>` automatically, so don’t just copy and paste the whole thing.

Listing 25: Adding links to the Learn Enough Twitter account.`index.html`

```
      .
      .
      .
      for our official email list</a> now.
    </p>

    <p>
      <a href="http://twitter.com/learnenough" target="_blank"
      style="text-decoration: none;">
        <img src="FILL_IN">
      </a>
      You should follow Learn Enough on Twitter
      <a href="http://twitter.com/learnenough" target="_blank">here</a>.
    </p>
    .
    .
    .

```

## [3More pages, more tags](https://www.learnenough.com/html-tutorial#sec-more_pages)

Having completed a full index page in [Section 2](https://www.learnenough.com/html-tutorial#sec-filling_in_the_index_page) (and having learned a bunch of HTML tags along the way), the time has now come to add a couple more pages to our website.This will give us a chance to learn some more useful HTML tags, while discovering some of the limitations of our purely hand-edited approach.

The first new addition will be a meta-page on HTML tags themselves, which will give us a chance to reinforce the preceding material as we build it. The second page includes a lighthearted report on *Moby-Dick*, one of the free books available on the [Softcover](http://softcover.io/)website. This second page especially lends itself to styling, a task we’ll take up in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles).

### [3.1An HTML page about HTML](https://www.learnenough.com/html-tutorial#sec-an_html_page_about_html)

We’ll start by adding a reference page to collect some of the HTML tags we’ve learned about so far. This means creating a new file, which we can do by creating a new tab (typically with ⌘N) and then saving it as `tags.html`. Another method, and a personal favorite, is to run `touch tags.html` at the command line and then use ⌘P to open it the editor.

Once you’ve created `tags.html`, by whatever method, fill it with the contents of [Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page).

Listing 26: Adding the beginning of a page on HTML tags.`tags.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Tags</title>
    <meta charset="utf-8">
  </head>
  <body>

    <h1>Important HTML tags</h1>

    <img src="images/storm_trooper_tagged.jpg" alt="Tagged Storm Trooper">

    <p>
      This page is designed as a quick reference for some of the common tags
      covered in <a href="http://learnenough.com/html-tutorial"><em>Learn
      Enough HTML to Be Dangerous</em></a>. In the process of making it, we'll
      learn how to make HTML <em>tables</em> via <code>table</code> and
      related tags.
    </p>

    <p>
      The tables below don't include all HTML tags, but they do list many of
      the most important ones.
    </p>

  </body>
</html>

```

Note that [Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page) involves repeating the HTML skeleton from [Listing 7](https://www.learnenough.com/html-tutorial#code-html_skeleton), which is an inconvenient duplication of effort. It also becomes increasingly annoying as the number of pages in a site grows, especially if (as is often the case) we need to make changes to the `head` of the document. We’ll deal with this issue the Right Way™ in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial) (using a so-called *templating system*), but for now we’ll just live with the annoyance.

[Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page) introduces one new tag, the minor but occasionally useful `code` tag:

```
<code>table</code>

```

Designed to display pieces of markup or source code, the `code` tag is rendered by most browsers in a monospace font, `like this`. (In a monospace font, all letters have the same width, which is especially convenient when lining up formatted code.)

The page defined by [Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page) won’t yet render as intended because of the `img` tag, which currently references a nonexistent image. To fix this, download the image (which is just a smaller version of the one in [Figure 4](https://www.learnenough.com/html-tutorial#fig-storm_trooper_tagged)) to the local disk:

```
$ curl -o images/storm_trooper_tagged.jpg \
>      -OL cdn.learnenough.com/storm_trooper_tagged.jpg

```

Note that the backslash `\` should be typed, but your shell will include `>` automatically, so don’t just copy and paste the whole thing.

The result appears in [Figure 37](https://www.learnenough.com/html-tutorial#fig-tags_page).

![images/figures/tags_page](https://ws2.sinaimg.cn/large/006tNc79gy1fm65juc1h6j30vj0ntq5y.jpg)

Figure 37: The beginning of an HTML tags page.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_an_html_page_about_html)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Does the HTML in [Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page) validate?
2. As with the kitten image, the Stormtrooper tag image is used under a Creative Commons license that requires attribution. By following the model in [Listing 23](https://www.learnenough.com/html-tutorial#code-image_link), fulfill this requirement by linking the image in [Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page) to the [original image URL](https://www.flickr.com/photos/jdhancock/3814523970).

### [3.2Tables](https://www.learnenough.com/html-tutorial#sec-tables)

Now that we’ve got a basic page set up, we’ll make a list of some of the tags we’ve learned about so far. Our plan is to indicate the exact HTML code for the tag, its name, and its purpose. The result is a *table* of information, so to display it we’ll use the HTML `table`tag. Because HTML tags divide broadly into *inline elements* and *block elements* ([Box 5](https://www.learnenough.com/html-tutorial#aside-inline_vs_block)), we’ll make a separate table for each type of tag.

> Box 5. Inline vs. block
>
> All of the elements on a page of HTML either flow with the text around them or interrupt the flow by creating a box of content that is separate from the other content on the page. The first category of tags is known as *inline*; the second category is called *block* ([Figure 38](https://www.learnenough.com/html-tutorial#fig-inline_vs_block)).
>
> All of the elements that modify text, such as `<strong>` and `<em>`, are inline elements, which makes sense since we wouldn’t want text to jump to a new line every time we made it bold or italic. Other common inline elements include links and (perhaps surprisingly) images. Inline elements take up only as much width on the page as is necessary to contain the content inside the tags—you can think of inline elements as being shrink-wrapped around the content inside them
>
> In contrast, block elements always start on a new line, as if there is a line break in front of them, so one of their main purposes is to divide the page’s text into different presentational groups, such as paragraphs or lists. Unlike inline elements, block elements bound the full width of the page, like an inflexible cardboard box.
>

![images/figures/paragraph_tag](https://ws2.sinaimg.cn/large/006tNc79gy1fm65k1g4ywj30jg0eo420.jpg)

Figure 38: Inline vs. block elements.

#### [Block elements](https://www.learnenough.com/html-tutorial#sec-block_elements)

A table is defined by opening and closing `table` tags, with each *table row* defined by the `tr` tag. Typically, the first row includes labels for the table’s columns via *table headers*, defined by the `th` tag, as shown in [Listing 27](https://www.learnenough.com/html-tutorial#code-table_headers).

Listing 27: Defining a table with headers.`tags.html`

```
    .
    .
    .
    <p>
      The tables below don't include all HTML tags, but they do list many of
      the most important ones.
    </p>

    <h2>Block Elements</h2>

    <table>
      <tr>
        <th>Tag</th>
        <th>Name</th>
        <th>Purpose</th>
      </tr>
    </table>
    .
    .
    .

```

The result of [Listing 27](https://www.learnenough.com/html-tutorial#code-table_headers) is shown in [Figure 39](https://www.learnenough.com/html-tutorial#fig-table_headers). Because the natural layout inside a file is vertical, whereas the display is horizontal, it can be challenging to mentally map table contents to the visual result, but it gets easier with practice.

![images/figures/table_headers](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ldphgnj30vj0nt0wb.jpg)

Figure 39: Table headers.

After optionally defining the table headers, tables generally consist of a series of *table data* cells defined by the `td` tag. We can get started with the content of the table by adding a row for the heading tags first introduced in [Section 2.1](https://www.learnenough.com/html-tutorial#sec-headings). The result (which incidentally solves the exercise from [Section 2.1.1](https://www.learnenough.com/html-tutorial#sec-exercises_headings)) appears in [Listing 28](https://www.learnenough.com/html-tutorial#code-table_data_row).

Listing 28: Adding a row of data.`tags.html`

```
    .
    .
    .
    <p>
      The tables below don't include all HTML tags, but they do list many of
      the most important ones.
    </p>

    <h2>Block Elements</h2>

    <table>
      <tr>
        <th>Tag</th>
        <th>Name</th>
        <th>Purpose</th>
      </tr>
      <tr>
        <td><code>h1</code>&ndash;<code>h6</code></td>
        <td>headings</td>
        <td>include a heading (levels 1&ndash;6)</td>
      </tr>
    </table>
    .
    .
    .

```

[Listing 28](https://www.learnenough.com/html-tutorial#code-table_data_row) uses the `code` tag we saw in [Listing 26](https://www.learnenough.com/html-tutorial#code-tags_page), and also introduces uses `&ndash;`, which is “[character entity reference](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references)” for an *en dash* (a dash roughly the width of the letter “n”, like this: –). Because our HTML document uses the `utf-8` character set ([Listing 7](https://www.learnenough.com/html-tutorial#code-html_skeleton)), we could also use a literal en dash –, but the entity reference is common, and it’s good to know how to use both.

This is a lot to handle at once, which makes it good practice for learning to visualize the result of HTML markup. Once you have a guess in your mind’s eye, you can refresh your browser to see the result ([Figure 40](https://www.learnenough.com/html-tutorial#fig-table_data_row)).

![images/figures/table_data_row](https://ws1.sinaimg.cn/large/006tNc79gy1fm65lqchf3j30vj0nt77n.jpg)

Figure 40: Adding a row of table data.

We’ve now seen the most important table tags, so we’re ready to fill in the table with rows for the other block-level tags we’ve seen so far. These include `p` and the table tags themselves.[17](https://www.learnenough.com/html-tutorial#cha-0_footnote-17) The result appears in [Listing 29](https://www.learnenough.com/html-tutorial#code-block_elements_table).[18](https://www.learnenough.com/html-tutorial#cha-0_footnote-18)

Listing 29: A more complete table of HTML block elements.`tags.html`

```
    .
    .
    .
    <p>
      The tables below don't include all HTML tags, but they do list many of
      the most important ones.
    </p>

    <h2>Block Elements</h2>

    <table>
      <tr>
        <th>Tag</th>
        <th>Name</th>
        <th>Purpose</th>
      </tr>
      <tr>
        <td><code>h1</code>&ndash;<code>h6</code></td>
        <td>headings</td>
        <td>include a heading (levels 1&ndash;6)</td>
      </tr>
      <tr>
        <td><code>p</code></td>
        <td>paragraph</td>
        <td>include a paragraph of text</td>
      </tr>
      <tr>
        <td><code>table</code></td>
        <td>table</td>
        <td>include a table</td>
      </tr>
      <tr>
        <td><code>tr</code></td>
        <td>table row</td>
        <td>include a row of data</td>
      </tr>
      <tr>
        <td><code>th</code></td>
        <td>table header</td>
        <td>make a table header</td>
      </tr>
      <tr>
        <td><code>td</code></td>
        <td>table data</td>
        <td>include a table data cell</td>
      </tr>
    </table>
    .
    .
    .

```

There are a lot of new rows in [Listing 29](https://www.learnenough.com/html-tutorial#code-block_elements_table), so you can copy and paste if you want, but you’ll learn more by typing in the tags by hand. (You’ll find that it can be quite cumbersome, which is one reason many real-world tables are generated from databases using programming languages like Ruby.) The result appears in [Figure 41](https://www.learnenough.com/html-tutorial#fig-block_elements_table).

![images/figures/block_elements_table](https://ws2.sinaimg.cn/large/006tNc79gy1fm65m4upmcj30vj0nt0wo.jpg)

Figure 41: A table for some HTML block elements.

By the way, you might notice in [Figure 41](https://www.learnenough.com/html-tutorial#fig-block_elements_table) that the spacing around the table data cells isn’t ideal. This is exactly the kind of detail that is handled by Cascading Style Sheets (as covered in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial)).

#### [Inline elements](https://www.learnenough.com/html-tutorial#sec-inline_elements)

Now that we know how to make a basic table, we’re ready to add a new table of inline elements as well. Because inline elements by definition don’t start a new line, it’s easy to include examples of the tags along with their definitions. For example, we can include a working example of the `em` tag, as shown in [Listing 30](https://www.learnenough.com/html-tutorial#code-beginning_inline_table).

Listing 30: A start at a table of inline tags.`tags.html`

```
.
.
.
   <h2>Inline Elements</h2>

    <table>
      <tr>
        <th>Tag</th>
        <th>Name</th>
        <th>Purpose</th>
        <th>Example</th>
        <th>Result</th>
      </tr>
      <tr>
        <td><code>em</code></td>
        <td>emphasized</td>
        <td>make emphasized text</td>
        <td><code>&lt;em&gt;technical sophistication&lt;/em&gt;</code></td>
        <td><em>technical sophistication</em></td>
      </tr>
    </table>
.
.
.

```

[Listing 30](https://www.learnenough.com/html-tutorial#code-beginning_inline_table) introduces the solution to the tricky problem of displaying literal angle brackets, which arranges for the browser to display, e.g., <em>technical sophistication</em> rather than *technical sophistication*. The way to do it is by “escaping out” `<` and `>` with the HTML [character entities](http://www.w3schools.com/html/html_entities.asp) `&lt;` (“less than”) and `&gt;` (“greater than”). The result appears in [Figure 42](https://www.learnenough.com/html-tutorial#fig-beginning_inline_table).

![images/figures/beginning_inline_table](https://ws1.sinaimg.cn/large/006tNc79gy1fm65mk7m92j30vj0nttd9.jpg)

Figure 42: A good start at a table of inline elements.

Some other inline elements we’ve encountered so far are `strong`, `a`, `img`, and `code`.Adding them to the table in [Listing 30](https://www.learnenough.com/html-tutorial#code-beginning_inline_table) is left as an exercise. Either before or after doing that exercise, I suggest adding and committing the changes and then pushing up to GitHub Pages:

```
$ git add -A
$ git commit -m "Add a tags page"
$ git push

```

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_tables)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Follow the template in [Listing 31](https://www.learnenough.com/html-tutorial#code-add_strong_table) to add information on the `strong`, `a`, and `img` tags. Why does the `img` tag example use the Bitly link shortener?
2. Add an additional row for the `code` tag. Does the page validate?

Listing 31: Template for adding `strong`, `a`, and `img` tags.`tags.html`

```
    .
    .
    .
    <h2>Inline Elements</h2>

    <table>
      <tr>
        <th>Tag</th>
        <th>Name</th>
        <th>Purpose</th>
        <th>Example</th>
        <th>Result</th>
      </tr>
      <tr>
        <td><code>em</code></td>
        <td>emphasized</td>
        <td>make emphasized text</td>
        <td><code>&lt;em&gt;technical sophistication&lt;/em&gt;</code></td>
        <td><em>technical sophistication</em></td>
      </tr>
      <tr>
        <td><code>strong</code></td>
        <td>strong</td>
        <td>make strong text</td>
        <td>
          <code>&lt;strong&gt;at least a billion people&lt;/strong&gt;</code>
        </td>
        <td>FILL_IN</td>
      </tr>
      <tr>
        <td><code>a</code></td>
        <td>anchor</td>
        <td>make hyperlink</td>
        <td>
          <code>
            &lt;a href="http://learnenough.com/"&gt;Learn Enough&lt;/a&gt;
          </code>
        </td>
        <td>FILL_IN</td>
      </tr>
      <tr>
        <td><code>img</code></td>
        <td>image</td>
        <td>include an image</td>
        <td>
          <code>
            &lt;img src="https://bit.ly/1MZAFuQ" alt="Michael Hartl"&gt;
          </code>
        </td>
        <td>FILL_IN</td>
      </tr>
    </table>
    .
    .
    .

```

### [3.3Divs and spans](https://www.learnenough.com/html-tutorial#sec-divs_and_spans)

Having created a new page for our HTML table experiment, we’re now ready to make a third page for our sample website. We’ll add some initial content while blocking out the structure with three new tags: `header`, `div` (for *division*), and `span`. These tags have little to no impact on the page appearance, but they help us organize the page and its contents into logical units. All three tags, and especially `div`s and `span`s, are heavily used when styling web pages using CSS ([*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial)).We’ll get a preview of this practice when applying inline styles in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles).

The page itself will take the form of a mock book report on the classic American whaling novel *Moby-Dick*, which among other places is available in a [free Softcover edition](https://www.softcover.io/read/6070fb03/moby-dick). As we’ll see in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles), this content will especially lend itself to styling.

The first thing you should do is create a file called `moby_dick.html`. Then, because it’s never wrong to include pictures of animals (even non-cats!) on web pages, we’ll include a picture of sperm whales ([Figure 43](https://www.learnenough.com/html-tutorial#fig-sperm_whales))[19](https://www.learnenough.com/html-tutorial#cha-0_footnote-19) to go along with our report. We’ll also include an image for the book’s cover ([Figure 44](https://www.learnenough.com/html-tutorial#fig-moby_dick_cover)).

![sperm_whales](https://ws1.sinaimg.cn/large/006tNc79gy1fm65mnum26j30m80b875n.jpg)

Figure 43: A pod of sperm whales.

![images/figures/moby_dick](https://ws2.sinaimg.cn/large/006tNc79gy1fm65mtqz7vj307s0boq3x.jpg)

Figure 44: The cover image for *Moby-Dick*.

In order to include the images on our web page, we need to download them to the local machine (as we did with the kitten image in [Section 2.4](https://www.learnenough.com/html-tutorial#sec-images)):

```
$ curl -o images/sperm_whales.jpg -OL cdn.learnenough.com/sperm_whales.jpg
$ curl -o images/moby_dick.png    -OL cdn.learnenough.com/moby_dick.png

```

The initial book report page is fairly long, which makes it an excellent exercise in reading and writing HTML. The result, which highlights a few especially important lines, appears in [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick). Note especially the use of `target="_blank"`, which arranges to open links in a new browser tab.[20](https://www.learnenough.com/html-tutorial#cha-0_footnote-20) There is also one intentional error in [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick); catching and fixing it is left as an exercise ([Section 3.3.1](https://www.learnenough.com/html-tutorial#sec-exercises_divs_and_spans)).

Listing 32: The initial *Moby-Dick* book report.`moby_dick.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>Moby Dick</title>
    <meta charset="utf-8">
  </head>
  <body>

    <!-- much here to be styled, will do so in last section -->
    <header>
      <h1>A Softcover Book Report</h1>
      <h2>Moby-Dick (or, The Whale)</h2>
    </header>

    <div>
      <p>
        The <a href="http://www.softcover.io/">Softcover</a> publishing platform
        was designed mainly for ebooks like the
        <a href="http://railstutorial.org/book"><em>Ruby on Rails Tutorial</em>
        book</a> and <a href="http://learnenough.com/html"><em>Learn Enough
        HTML to Be Dangerous</em></a>, but it's also good for making more
        traditional books, such as the novel <em>Moby-Dick</em> by Herman
        Melville (sometimes written as <em>Moby Dick</em>). We present below a
        short and affectionately irreverent book report on this classic of
        American literature.
      </p>
    </div>

    <a href="https://commons.wikimedia.org/wiki/File:Sperm_whale_pod.jpg">
      <img src="images/sperm_whales.jpg">
    </a>

    <div>

      <h3>Moby-Dick: A classic tale of the sea</h3>

      <a href="https://www.softcover.io/read/6070fb03/moby-dick"
         target="_blank">
        <img src="images/moby_dick.png" alt="Moby Dick">
      </a>

      <p>
        <a href="https://www.softcover.io/read/6070fb03/moby-dick"
           target="_blank">
          <em>Moby-Dick</em></a>
          by Herman Melville begins with these immortal words:
      </p>

      <blockquote>
        <p>
          <span>Call me Ishmael.</span> Some years ago–never mind how long
          precisely–having little or no money in my purse, and nothing
          particular to interest me on shore, I thought I would sail about a
          little and see the watery part of the world. It is a way I have of
          driving off the spleen and regulating the circulation.
        </p>
      </blockquote>

      <p>
        After driving off his spleen (which <em>can't</em> be good for you),
        Ishmael then goes on in much the same vein for approximately one
        jillion pages. The only thing bigger than Moby Dick (who—<em>spoiler
        alert!</em>—is a giant white whale) is the book itself.
      </p>
    </div>
  </body>
</html>

```

In [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick), the `header` tag contains the `h1` and `h2` tags, and its importance will become apparent only when we add inline styles in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles). For now, what’s important is that it’s an abstract semantic tag used to label a part of the page, and has no immediate effect on the page’s appearance.

Likewise, the `div` tag sets the page divisions apart, but won’t have any effect until [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles). We’ve also wrapped the iconic first line of *Moby-Dick*, “Call me Ishmael.”, in a `span` tag in anticipation of styling it in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles). (The main difference between the `div` and `span` tags is that `div` is a block element, whereas `span` is an inline element ([Box 5](https://www.learnenough.com/html-tutorial#aside-inline_vs_block)).) Finally, we’ve introduced the `blockquote` tag for quoting blocks of text.

In addition to illustrating the `header`, `div`, and `span` tags, [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick) also shows an HTML *comment*, which appears as follows:[21](https://www.learnenough.com/html-tutorial#cha-0_footnote-21)

```
<!-- much here to be styled, will do so in last section -->

```

This line, which foreshadows the styling steps in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles), is ignored by the browser, and is *not* visible on the rendered page, as (not) seen in [Figure 45](https://www.learnenough.com/html-tutorial#fig-initial_moby_dick).[22](https://www.learnenough.com/html-tutorial#cha-0_footnote-22)

![images/figures/initial_moby_dick](https://ws1.sinaimg.cn/large/006tNc79gy1fm65myq769j30vj0ntn80.jpg)

Figure 45: The initial Softcover book report on *Moby-Dick*.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_divs_and_spans)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Validate the HTML in [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick) and confirm that there’s one warning and one error. Apply the fixes suggested by the validator and confirm that the new page validates with no warnings.
2. In the previous exercise, you should have found a warning that suggested setting the language of the page to English. Update the site’s other pages with the same change. (This repetition of effort is inconvenient, and would be handled automatically by a templating system.)
3. Add `header`, `div`, and `span` to the tables in `tags.html`. *Hint*: Like `div`, `header` is a block element.

### [3.4Lists](https://www.learnenough.com/html-tutorial#sec-lists)

As part of our mini-report on *Moby-Dick*, we’d like to include a couple of lists with some of our observations about the book. As we’ll see, HTML lists come in two basic types.

The first list will highlight our top three favorite things about *Moby-Dick*. Because we want these to be in rank-order, we’ll use the *ordered list* tag `ol`:

```
<h4>Our top 3 favorite things about Moby Dick</h4>

<ol>
  <li>Vengeful whale</li>
  <li>Salty sailors</li>
  <li>The names "Queequeg" and "Starbuck"</li>
</ol>

```

Here the `li` tag indicates a **li**st element, and the result will be numbered in sequence:

```
1. …
2. …
3. …

```

The second list will contain some other miscellaneous musings. Because the order isn’t important, we’ll use the *unordered list* tag `ul`, together with the same `li` list element tag used for ordered lists:

```
<h4>Other things about Moby Dick</h4>

<ul>
  <li>
    Chapter after chapter (after chapter) of meticulous detail about whaling
  </li>
  <li>
    The story pretty much
    <a href="https://en.wikipedia.org/wiki/Essex_(whaleship)"
       target="_blank">happened in real life</a>
  </li>
  <li>Mad sea captains are fun</li>
</ul>

```

As we’ll see in a moment, unordered list elements are styled as bullet points by default:

```
• …
• …
• …

```

They are much more useful than this, though, and in practice unordered lists are used for significantly more than just making bullet points (as we’ll see in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial)).

Putting these two lists together and adding them to the end of `moby_dick.html` gives [Listing 33](https://www.learnenough.com/html-tutorial#code-moby_dick_lists).

Listing 33: Adding lists to our *Moby-Dick* book report.`moby_dick.html`

```
      .
      .
      .
      <h4>My top 3 favorite things about Moby Dick</h4>

      <ol>
        <li>Vengeful whale</li>
        <li>Salty sailors</li>
        <li>The names "Queequeg" and "Starbuck"</li>
      </ol>

      <h4>Other things about Moby Dick</h4>

      <ul>
        <li>
          Chapter after chapter (after chapter) of meticulous detail about
          whaling
        </li>
        <li>
          The story pretty much
          <a href="https://en.wikipedia.org/wiki/Essex_(whaleship)"
             target="_blank">happened in real life</a>
        </li>
        <li>Mad sea captains are fun</li>
      </ul>
    </div>
  </body>
</html>

```

The result appears in [Figure 46](https://www.learnenough.com/html-tutorial#fig-moby_dick_lists), which incidentally also shows the rendered `blockquote` that’s not quite visible in [Figure 45](https://www.learnenough.com/html-tutorial#fig-initial_moby_dick).

![images/figures/moby_dick_lists](https://ws2.sinaimg.cn/large/006tNc79gy1fm65n3ktisj30vk0ntwk5.jpg)

Figure 46: Ordered and unordered lists.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_lists)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Add `ol`, `ul`, and `li` tags to `tags.html`. Which are block elements are which are inline?

### [3.5A navigation menu](https://www.learnenough.com/html-tutorial#sec-a_navigation_menu)

Before moving on to styling our book report page in [Section 4](https://www.learnenough.com/html-tutorial#sec-inline_styles), we’ll add a component common to most sites on the Web, yet one whose origins are mysterious: a navigation menu with links to all the pages on the site ([Box 6](https://www.learnenough.com/html-tutorial#aside-hacked_together_with_perl)).[23](https://www.learnenough.com/html-tutorial#cha-0_footnote-23) In the process, we’ll learn how to make links to pages on the current site instead of always linking to external websites. The navigation menu will also give us another chance to see how cumbersome it is to make websites without a templating system.

> Box 6. Hacked together with Perl
>
> Having watched the Web evolve from the start, I (Michael) knew how to make web pages from an early date, but I always wondered how it was that so many sites had the same menu on each page. I figured it must be some property of HTML I didn’t know about, but even an early book on web design didn’t cover it.
>
> I remember thinking, you don’t just hard-code the same menu on every page, do you? That’s seems like an awful lot of duplicated effort. And what if you want to change it?
>
> It turns out that no, well-made sites don’t require you to hard-code the menu everywhere. In fact, as I realized much later, most such sites at the time were just hacked together with [Perl](https://en.wikipedia.org/wiki/Perl) ([Figure 47](https://www.learnenough.com/html-tutorial#fig-perl)), but at the time it was a genuine mystery.(Although Perl is still in use, nowadays it’s probably more common to stitch websites together using PHP, Python, JavaScript, or Ruby. The principle, though, remains the same.)
>
> In the present tutorial, we’re not in a position to solve this problem the Right Way™, so we *will* have to write everything by hand. But this is a [feature, not a bug](https://www.learnenough.com/command-line-tutorial#aside-speak_geek), because solving the problem by hand helps us appreciate why it should be solved by a computer instead.
>
> We’ll reveal the solution to this mystery, called a *templating system*, in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial), and it’s covered thoroughly in the [Ruby on Rails Tutorial](http://railstutorial.org/) as well.
>

![lisp](https://ws3.sinaimg.cn/large/006tNc79gy1fm65n70wi6j30kk064dha.jpg)

Figure 47: Hacking most of it together with Perl. (“[Lisp](http://xkcd.com/)” via [xkcd](http://xkcd.com/).)

We’ll start by adding a `div` containing three links to the index page ([Listing 34](https://www.learnenough.com/html-tutorial#code-index_menu)). Note that we’ve adopted the common convention of referring to the index page as “Home”.

Listing 34: Adding navigation links.`index.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>Learn Enough to Be Dangerous</title>
    <meta charset="utf-8">
  </head>
  <body>

    <div>
      <a href="index.html">Home</a>
      <a href="moby_dick.html">Moby Dick</a>
      <a href="tags.html">HTML Tags</a>
    </div>

    <h1>The Learn Enough Story</h1>
    .
    .
    .

```

We see from [Listing 34](https://www.learnenough.com/html-tutorial#code-index_menu) that the way to link to a local page simply involves setting the `href` attribute equal to the path to the file, which works exactly the same way as an `img` tag’s `src` attribute ([Section 2.4](https://www.learnenough.com/html-tutorial#sec-images)):

```
<a href="tags.html">HTML Tags</a>

```

The result appears in [Figure 48](https://www.learnenough.com/html-tutorial#fig-index_menu).

![images/figures/index_menu](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ncim2dj30vj0nt4gj.jpg)

Figure 48: The navigation menu on the index page.

We can add the same menu to the HTML tags page with the markup in [Listing 35](https://www.learnenough.com/html-tutorial#code-tags_menu). The result appears in [Figure 49](https://www.learnenough.com/html-tutorial#fig-tags_menu).

Listing 35: Adding the navigation menu to the HTML tags page.`tags.html`

```
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Tags</title>
    <meta charset="utf-8">
  </head>
  <body>

    <div>
      <a href="index.html">Home</a>
      <a href="moby_dick.html">Moby Dick</a>
      <a href="tags.html">HTML Tags</a>
    </div>

    <h1>Important HTML tags</h1>
    .
    .
    .

```

Adding the menu to the page on Moby Dick is left as an exercise.

![images/figures/tags_menu](https://ws1.sinaimg.cn/large/006tNc79gy1fm65ngue3hj30vj0ntaey.jpg)

Figure 49: The navigation menu on the HTML tags page.

By the way, you may have noticed that it would probably be more natural to order the navigation in order of the pages’ introduction, i.e., Home, Tags, Moby Dick. Changing this order is also left as an exercise, mainly so that you feel the pain of making the same change on three different pages—a pain that is alleviated by the templating systems covered in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial). Either before or after doing that exercise, I suggest adding and committing the changes and then pushing up to GitHub Pages:

```
$ git add -A
$ git commit -m "Add a Moby Dick page and a menu"
$ git push

```

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_a_navigation_menu)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Add the menu links to the Moby Dick page.
2. In the menu links, change the order of the links so that the tags page comes second. How many files do you have to edit?

## [4Inline styling](https://www.learnenough.com/html-tutorial#sec-inline_styles)

Now that we’ve added the content for our pages and blocked out the basic structure, we’re ready to add some styling. Our basic approach involves adding *inline styles*, which means putting styling commands directly inside the site’s HTML tags. This approach will allow us to understand exactly what our styling is doing on a per-element basis, giving us immediate results without the overhead of adding Cascading Style Sheets. Moreover, inline and CSS styling commands are essentially the same, so everything we cover here is applicable to the industrial-grade styling covered in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial) ([Box 7](https://www.learnenough.com/html-tutorial#aside-separation_styles)).

As mentioned in [Section 3.3](https://www.learnenough.com/html-tutorial#sec-divs_and_spans), our design efforts will focus on the *Moby-Dick* book report page, which stands to gain the most from changing the default HTML styling.

> Box 7. Separating style and content
>
> If adding styles directly to elements gives you the results that you want, why is it considered bad practice to do it?
>
> One reason is that when your styling is kept in a separate file from your content and layout, the HTML files are cleaner and easier to maintain. This doesn’t make a huge difference when one developer is working on a single page, but when you have multiple developers all making changes to multiple pages, it quickly becomes a nightmare to make changes efficiently and consistently. Imagine if you decided that you didn’t like the size of a font on your site, and had to go around to every place on every page that needed a new style. If this were the only way, no one would ever do it.
>
> Another reason for separating style from content is that it allows for much greater flexibility and efficiency when applying style rules to multiple elements. Instead of having to style each individual tag, we can apply styling to all elements on the entire site, or just to certain elements that we choose.
>
> For instance, it’s possible to make a table span the full width of the page using the rule `width: 100%`. If we wanted *every* table on the site to have the same styling, we would have to copy and paste that into every `<table>` tag on every page:
>
> ```
>   <table style="width: 100%;">
>   <table style="width: 100%;">
>   <table style="width: 100%;">
> ```
>
> With CSS, we can tell the browser to style every table with a small bit of code.
>
> ```
>   table {
>     width: 100%;
>   }
> ```
>
> This represents a massive gain in simplicity and efficiency.
>
> Finally, every page on the Internet is sitting on a remote server somewhere sending data to the users visiting the site. Every word or line of code that you add to a page is something extra that needs to be downloaded over the network.Cutting out repetitive elements on a page makes them smaller, and thus helps sites load faster as well.
>

### [4.1Text styling](https://www.learnenough.com/html-tutorial#sec-text_style)

We’ll begin by adding a little styling to the quote of the first paragraph from *Moby-Dick*.Recall from [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick) that the quote uses the `blockquote` tag, which is set apart from the surrounding text by extra space and indentation ([Figure 50](https://www.learnenough.com/html-tutorial#fig-default_blockquote)).

![images/figures/default_blockquote](https://ws2.sinaimg.cn/large/006tNc79gy1fm65no4dlmj30vk0ntq7y.jpg)

Figure 50: The default blockquote styling.

To make the quote stand out even more, let’s change the font style to *italics* while increasing the font size to 20 pixels (`20px`). The way to do this is with the `style`attribute, which can be added to virtually any HTML tag. In this case, we’ll change the `font-style` and the `font-size` as follows:

```
<blockquote style="font-style: italic; font-size: 20px;">

```

Note that the styling rules after `style=` is a single string of characters, with each individual style separated from the others by a semicolon `;`. (The final semicolon isn’t technically necessary, but including it is a good practice since it lets us add additional styles later on without having to remember to add a semicolon.)

Taking this idea and editing `moby_dick.html` leads to the HTML shown in [Listing 36](https://www.learnenough.com/html-tutorial#code-styled_blockquote).The result appears in [Figure 51](https://www.learnenough.com/html-tutorial#fig-styled_blockquote).

Listing 36: Styling the blockquote.`moby_dick.html`

```
      .
      .
      .
      <blockquote style="font-style: italic; font-size: 20px;">
        .
        .
        .
      </blockquote>
      .
      .
      .

```

![images/figures/styled_blockquote](https://ws2.sinaimg.cn/large/006tNc79gy1fm65ntfeozj30vk0ntaf3.jpg)

Figure 51: A styled blockquote.

Next, we’ll add some styling to the famous first line “Call me Ishmael.” We’ll first revert the font style back to normal (which is how you emphasize text when the surrounding text is already in italics). Then we’ll make the font even bigger that the `20px` used for the rest of the quote, while also making it **bold**. Finally, we’ll change the color to an attention-grabbing **red**.

Ordinarily, there would be no way to style just the line “Call me Ishmael.” If we had written it as

```
Call me Ishmael. Some years ago…

```

at this point we’d be out of luck. Recall from [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick), though, that the opening line is wrapped in a `span` tag:

```
<span>Call me Ishmael.</span> Some years ago…

```

The reason for this is that we correctly anticipated wanting to style it later on. (In practice we can’t always anticipate such things, but of course we can wrap the relevant text in a `span` tag as needed.)

Although the `span` tag doesn’t really do anything by itself, we *can* add styles to it, as follows:

```
<span style="font-style: normal; font-size: 24px; font-weight: bold;
color: #ff0000;">Call me Ishmael.</span>

```

Here we’ve combined `font-style`, `font-size`, `font-weight`, and `color` to obtain the results outlined above. These are but a few of the many style properties available, which you can learn about at sites like [w3schools](http://www.w3schools.com/cssref/). Meanwhile, the color `ff0000` is a hexadecimal code for red, as discussed in [Box 8](https://www.learnenough.com/html-tutorial#aside-html_color).

> Box 8. HTML and hexadecimal color
>
> HTML colors are typically indicated using a system known as *hexadecimal RGB*(for “red, green, blue”), which gives us a flexible way to specify colors with fine-grained precision.
>
> Hexadecimal refers to the use of *base 16*, which uses 16 symbols from `0` to `F` to specify the decimal numbers 0 through 15:
>
> | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   |
> | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
> | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | A    | B    | C    | D    | E    | F    |
>
> Just as base 10 lets us count from 00 to 102−1=99102−1=99 using only two digits, hexadecimal lets us count from 00 to 162−1=255162−1=255 using `00` = 0 up to `FF` = 255.
>
> A computer monitor displays colors by combining red, green, and blue pixels together, which represent the three [additive primary colors](https://en.wikipedia.org/wiki/Primary_color). If all three colors are turned on, which would look like `#FFFFFF`, the screen will look white.Conversely, if all three colors are turned off, which is `#000000`, the screen will look black. Intermediate combinations of the three colors combine to produce virtually all the colors you can see:
>
> ![images/figures/hex](https://ws3.sinaimg.cn/large/006tNc79gy1fm65nvbj8jj30vk0ntaf3.jpg)
>
> For convenience, HTML also supports a shorthand that can stand in for the full hex string in some cases. For example, if the numbers are repeated, as in `#222222`, `#bbbbbb`, or `#aa22ff`, you can shorten the whole number to just three digits, like this: `#222`, `#bbb`, or `#a2f`. (Note that we’ve switched to lower-case letters, which is more common in modern HTML code, but is exactly equivalent the upper-case versions shown above.) When the browser sees only three digits, it fills in the missing ones automatically.
>
> The hexadecimal color system might seem confusing at first, but you’ll find that you quickly come to understand how the three values work together to make different colors (and different shades of those colors). To learn more, we suggest playing around with a [color picker](https://www.google.com/search?q=color+picker) to see what kinds of colors you can make.
>

Including the styles above in `moby_dick.html` gives us the code in [Listing 37](https://www.learnenough.com/html-tutorial#code-styled_span), with the result shown in [Figure 52](https://www.learnenough.com/html-tutorial#fig-styled_span).

Listing 37: Adding style to the opening span.`moby_dick.html`

```
      .
      .
      .
      <blockquote style="font-style: italic; font-size: 20px;">
        <p>
          <span style="font-style: normal; font-size: 24px; font-weight: bold;
          color: #ff0000;">Call me Ishmael.</span>
          Some years ago–never mind how long precisely–having little or
          no money in my purse, and nothing particular to interest me on shore,
          I thought I would sail about a little and see the watery part of the
          world. It is a way I have of driving off the spleen and regulating the
          circulation.
        </p>
      </blockquote>
      .
      .
      .

```

![images/figures/styled_span](https://ws3.sinaimg.cn/large/006tNc79gy1fm65nytocxj30vk0ntgqn.jpg)

Figure 52: Making the opening line really pop.

As a final change, we’ll align the text of the book report headers so that it’s centered in the page. The way to do this is with the `text-align` property, as shown in [Listing 38](https://www.learnenough.com/html-tutorial#code-centered_headings).(Note that [Listing 38](https://www.learnenough.com/html-tutorial#code-centered_headings) also removes the comment from [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick) since it’s now obsolete.)

Listing 38: Centering the headings.`moby_dick.html`

```
    .
    .
    .

    <header>
      <h1 style="text-align: center;">A Softcover Book Report</h1>
      <h2 style="text-align: center;">Moby-Dick (or, The Whale)</h2>
    </header>
    .
    .
    .

```

The result appears in [Figure 53](https://www.learnenough.com/html-tutorial#fig-centered_headings).

![images/figures/centered_headings](https://ws2.sinaimg.cn/large/006tNc79gy1fm65o3ilufj30vj0ntwpr.jpg)

Figure 53: Centered headings.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_text_style)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Verify that `color: red;` has the same effect as `color: #ff0000;`. What are the advantages of each approach?
2. What would you guess the color of `#cccccc` is? Temporarily modify the color of the `span` in [Listing 37](https://www.learnenough.com/html-tutorial#code-styled_span) to check your guess. How does it differ from `#ccc`?

### [4.2Floats](https://www.learnenough.com/html-tutorial#sec-float)

Now that we’ve learned how to move text around, let’s look at how to adjust how other elements on the page can be moved. We’ll start by shrinking the size of the cover image down a little, and then we’ll arrange for the text to flow around it as if it were part of the paragraphs and blockquote.

We’ll start by using the `height` attribute to the `img` tag to restrict the height to 200 pixels:

```
<img src="images/moby_dick.png" alt="Moby Dick" height="200px">

```

Several caveats are in order here. First, although inline resizing is still fairly common, using CSS is the best practice. Second, resizing the image this way (whether inline or with CSS) affects only the image *display*, and the entire image still needs to be downloaded from the web server, so this technique should be used only for fairly minor resizings.[24](https://www.learnenough.com/html-tutorial#cha-0_footnote-24) (If you’ve ever visited a web page where a seemingly tiny image takes *forever* to download, this is probably the reason why.) Finally, if you go this route you should use *either* `height` *or* `width`, but not both, as the combination forces the browser to attempt to respect both numbers, which can result in weird image resizing effects ([Figure 54](https://www.learnenough.com/html-tutorial#fig-bad_image)).

![images/figures/image_bad](https://ws2.sinaimg.cn/large/006tNc79gy1fm65o8340sj30sa0bmtcv.jpg)

Figure 54: Bad image resizing is bad.

In order to get the text to flow around the image, we need to use a style technique called *floating*. The idea is that when you set an element to “float” to the left or right (there is no center), all the inline content around it will flow around the floated element. To see this in action, all we need to do is add `style="float: left;"` to the image attributes:

```
<img src="images/moby_dick.png" alt="Moby Dick" height="200px"
style="float: left;">

```

Inserting this into the book report page gives [Listing 39](https://www.learnenough.com/html-tutorial#code-image_resize_float), with the result shown in [Figure 55](https://www.learnenough.com/html-tutorial#fig-image_resize_float).

Listing 39: Resizing and floating an image.`moby_dick.html`

```
      .
      .
      .
      <h3>Moby-Dick: A classic tale of the sea</h3>

      <a href="https://www.softcover.io/read/6070fb03/moby-dick"
         target="_blank">
        <img src="images/moby_dick.png" alt="Moby Dick" height="200px"
        style="float: left;">
      </a>
      .
      .
      .

```

In [Figure 55](https://www.learnenough.com/html-tutorial#fig-image_resize_float), the image is effectively treated like text, with the normal text now flowing up and to its side. We’ll see in [Section 4.5](https://www.learnenough.com/html-tutorial#sec-struct_box_styles) that the `float` attribute also arranges for the text to flow past the image as well.

![images/figures/image_resize_float](https://ws2.sinaimg.cn/large/006tNc79gy1fm65odnpf0j30vk0ntdos.jpg)

Figure 55: A nicely resized & floated image.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_float)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. What happens if you change `float: left` to `float: right` in [Listing 39](https://www.learnenough.com/html-tutorial#code-image_resize_float)?

### [4.3Applying a margin](https://www.learnenough.com/html-tutorial#sec-struct_margin)

Even though we’ve floated the image, the page still looks a little weird, with the text smashed up against the book cover. To make it look better, we’ll add a *margin* of empty space to the right of the image.

Margins are one of three styles that can be applied to the imaginary boxes that contain HTML content, the others being *padding* (empty space inside the box) and *borders* (a line around the box). We’ll talk more about these styles in the context of the *box model*covered in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial), but we can accomplish our immediate goal by applying a margin using inline styling. (We’ll see an example of padding in [Section 4.5](https://www.learnenough.com/html-tutorial#sec-struct_box_styles).)

We’ll start with the simplest kind of margin declaration, which looks like `margin: 40px;`:

```
<img src="images/moby_dick.png" alt="Moby Dick" height="200px"
style="float: left; margin: 40px;">

```

If we add this to the `img` tag ([Listing 40](https://www.learnenough.com/html-tutorial#code-margin_all)), everything surrounding the image moves 40 pixels in each direction, as shown in [Figure 56](https://www.learnenough.com/html-tutorial#fig-margin_all).

Listing 40: Adding an image margin.`moby_dick.html`

```
      .
      .
      .
      <h3>Moby-Dick: A classic tale of the sea</h3>

      <a href="https://www.softcover.io/read/6070fb03/moby-dick"
         target="_blank">
        <img src="images/moby_dick.png" alt="Moby Dick" height="200px"
        style="float: left; margin: 40px;">
      </a>
      .
      .
      .

```

![images/figures/margin_all](https://ws2.sinaimg.cn/large/006tNc79gy1fm65oium9dj30vk0ntn6l.jpg)

Figure 56: Close, but not quite!

[Figure 56](https://www.learnenough.com/html-tutorial#fig-margin_all) shows that we’ve gotten closer to our goal by putting some space between the text and the image, but styling still isn’t quite what we want. The reason is that writing `margin: 40px;` applies the margin in *all* directions, but we really only want the margin on the right side of the image, to separate it from the text.

The most general way to control where the margin goes is to give the `margin` attribute *four* values, corresponding to the top, right, bottom, and left of the box ([Figure 57](https://www.learnenough.com/html-tutorial#fig-margin_short)).

![images/figures/margin_short](https://ws1.sinaimg.cn/large/006tNc79gy1fm65om4ogkj30wq0fj0tf.jpg)

Figure 57: Think of the four values as going clockwise from the top.

For example, to get margins of 40, 30, 20, and 10 pixels going around an image (clockwise from the top), we could use this `style` attribute:

```
<img src="…" style="margin: 40px 30px 20px 10px;">

```

In the present case, we want only a right margin, so we can set the other three sides to `0px` (or just `0` for short):[25](https://www.learnenough.com/html-tutorial#cha-0_footnote-25)

```
<img src="images/moby_dick.png" alt="Moby Dick" height="200px"
style="float: left; margin: 0 40px 0 0;">

```

Applying this to the full source of the book report page gives [Listing 41](https://www.learnenough.com/html-tutorial#code-margin_right).

Listing 41: Adding only a right margin.`moby_dick.html`

```
      .
      .
      .
      <h3>Moby-Dick: A classic tale of the sea</h3>

      <a href="https://www.softcover.io/read/6070fb03/moby-dick"
         target="_blank">
        <img src="images/moby_dick.png" alt="Moby Dick" height="200px"
        style="float: left; margin: 0 40px 0 0;">
      </a>
      .
      .
      .

```

The result of [Listing 41](https://www.learnenough.com/html-tutorial#code-margin_right) shows exactly the result we want, with a margin applied only on the right.

![images/figures/margin_right](https://ws3.sinaimg.cn/large/006tNc79gy1fm65ornc46j30vk0ntn6f.jpg)

Figure 58: Much better!

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_struct_margin)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. How does the margin in [Listing 41](https://www.learnenough.com/html-tutorial#code-margin_right) change if we replace the margin with `margin-right: 40px`?
2. Add the style rule `padding: 10px;` to the `td` elements for the first two block elements in the table in `tags.html`. How annoying would it be to add them to every `td`? How annoying is changing from `10px` to `20px` everywhere? (This is one reason why in real life you always use CSS.)

### [4.4More margin tricks](https://www.learnenough.com/html-tutorial#sec-more_margin_tricks)

There are a couple of more margin tricks worth mentioning, both of which we can immediately put to good use. First, in addition to the shorthand `margin: 40px` (with only one value), it’s possible to include only two values:

```
margin: 20px 40px;

```

As illustrated in [Figure 57](https://www.learnenough.com/html-tutorial#fig-margin_short), this syntax sets the top and bottom margins to 20px and the left and right margins to 40px, so it is equivalent to

```
margin: 20px 40px 20px 40px;

```

This shorthand also works with just three values, like this: `margin: 20px 10px 40px;`. This is missing the last value, which (as seen in [Figure 57](https://www.learnenough.com/html-tutorial#fig-margin_short)) is the left margin. In this case, it will be filled in automatically from its opposite across the box (in this case, `10px`).

We can apply this to the header for the book report page by adding a bottom margin via `margin: 0 0 80px` as shown in [Listing 42](https://www.learnenough.com/html-tutorial#code-centered_header).

Listing 42: Centering the book report headers.`moby_dick.html`

```
    .
    .
    .
    <header style="text-align: center; margin: 0 0 80px;">
      <h1>A Softcover Book Report</h1>
      <h2>Moby-Dick (or, The Whale)</h2>
    </header>
    .
    .
    .

```

Note that we’ve also taken this opportunity to hoist the style `text-align: center` into the `header` tag. The result appears in [Figure 59](https://www.learnenough.com/html-tutorial#fig-margin_header).

![images/figures/margin_header](https://ws1.sinaimg.cn/large/006tNc79gy1fm65oy7fs3j30vk0ntqe6.jpg)

Figure 59: Adding a margin under the header.

The second margin trick is the use of `margin: auto;`, which inserts a margin with a size that is automatically the same on all sides. Its most common application is probably in the rule

```
margin: 0 auto;

```

which arranges for no top or bottom margin and automatic margins on the left and right.The result of equal left and right margins is that the element is *centered*, which is especially useful for elements like images that can’t be centered using the `text-align: center;` rule we saw in [Listing 38](https://www.learnenough.com/html-tutorial#code-centered_headings).

One restriction of `margin: 0 auto` is that it works only on block elements, but recall from [Box 5](https://www.learnenough.com/html-tutorial#aside-inline_vs_block) that the `img` tag is an inline element. We can fix this with the style `display: block;`, which overrides the default. Putting this together with the margin rule leads to [Listing 43](https://www.learnenough.com/html-tutorial#code-centered_image), with the result shown in [Figure 60](https://www.learnenough.com/html-tutorial#fig-centered_image).

Listing 43: A centered image.`moby_dick.html`

```
    .
    .
    .
    <a href="https://commons.wikimedia.org/wiki/File:Sperm_whale_pod.jpg">
      <img src="images/sperm_whales.jpg"
      style="display: block; margin: 0 auto;">
    </a>
    .
    .
    .

```

![images/figures/centered_image](https://ws1.sinaimg.cn/large/006tNc79gy1fm65p7geo4j30vj0ntal7.jpg)

Figure 60: A centered image.

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_more_margin_tricks)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. What happens if you use `margin: 0 auto` for the book cover image (together with `display: block`) without changing the float rule? What does this tell you about the precedence of the two rules?

### [4.5Box styling](https://www.learnenough.com/html-tutorial#sec-struct_box_styles)

So far, the changes we’ve made have had a relatively minor impact on the appearance of the book report page. In this section, we’ll see how a set of only four style rules can make a surprisingly big difference.

Recall from [Listing 32](https://www.learnenough.com/html-tutorial#code-initial_moby_dick) that we wrapped the bulk of the report in a `div` tag, which defines a block element that doesn’t get any default styling from the browser, thereby making it perfect to use as a wrapper for styling other content. In this case, we’ll use the `width` style to restrict the size of the main report to 500 pixels, and it turns out this lets us use the automatic margin trick from [Section 4.4](https://www.learnenough.com/html-tutorial#sec-more_margin_tricks) to center it using `margin: 20px auto` (thereby also putting a 20 pixel margin on the top and bottom). Finally, we’ll combine a `padding` rule with a change in the `background-color` using the hexadecimal color convention covered in [Box 8](https://www.learnenough.com/html-tutorial#aside-html_color). The resulting style rules appear in [Listing 44](https://www.learnenough.com/html-tutorial#code-box_styling).

Listing 44: Adding styling to the book report box.`moby_dick.html`

```
    .
    .
    .
    <div style="width: 500px; margin: 20px auto; padding: 30px;
    background-color: #fafafa;">

      <h3>Moby-Dick: A classic tale of the sea</h3>
    .
    .
    .

```

Comparing the before ([Figure 61](https://www.learnenough.com/html-tutorial#fig-box_before)) and after ([Figure 62](https://www.learnenough.com/html-tutorial#fig-box_after)) shows what a difference a few style rules can make.

![images/figures/box_before](https://ws4.sinaimg.cn/large/006tNc79gy1fm65plnrhbj30vk0ntgu7.jpg)

Figure 61: The report box before adding styling.

![images/figures/box_after](https://ws4.sinaimg.cn/large/006tNc79gy1fm65pzlokdj30vk0nt79o.jpg)

Figure 62: The report box after adding styling.

As we see in [Figure 62](https://www.learnenough.com/html-tutorial#fig-box_after), the report content has now been set apart from the rest of the page in a styled box.

To recap what happened, we set a width for the box, and because of this we were able to set the left and right margins to `auto`. Then we added padding to the box, which pushed the content inside away from the edges. (Investigating the difference between padding and margins is left as an exercise ([Section 4.5.1](https://www.learnenough.com/html-tutorial#sec-exercises_struct_box_styles)).) We also added a light gray background color with the hexadecimal code `#fafafa` ([Box 8](https://www.learnenough.com/html-tutorial#aside-html_color)). (Don’t worry about trying to visualize the color corresponding to a hex code; that’s what [color pickers](https://www.google.com/search?q=color+picker) are for.) Finally, because of the narrower width, the text of the *Moby-Dick* quote now flows around the floated cover image, thereby fulfilling the promise made at the end of [Section 4.2](https://www.learnenough.com/html-tutorial#sec-float).

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_struct_box_styles)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Temporarily change `padding` to `margin` in [Listing 44](https://www.learnenough.com/html-tutorial#code-box_styling). What difference does this make in the appearance?
2. Add and style a blockquote with padding and background color as shown in [Listing 45](https://www.learnenough.com/html-tutorial#code-lincoln_styled_blockquote). Fill in `TAG` with the right level tag for that location in the document, and replace `FILL_IN` with a reasonable color of your choice. The result for one color choice appears in [Figure 63](https://www.learnenough.com/html-tutorial#fig-lincoln_styled_blockquote).

Listing 45: Styling a famous quotation.`index.html`

```
    .
    .
    .
    <h1>The Learn Enough Story</h1>
    .
    .
    .
    <img src="images/kitten.jpg" alt="An adorable kitten">

    <TAG>Quotations</TAG>

    <p>
      In addition to hosting most of the world's supply of kitten videos, the
      Web is also full of inspiring quotes, perhaps none more so than this one:
    </p>

    <blockquote style="padding: 2px 20px; background: #FILL_IN;">
      <p>
        <em>Don't believe every quote you read on the Internet.</em>
        <br>
        —Abraham Lincoln
      </p>
    </blockquote>

    <h2>Background</h2>
    .
    .
    .

```

![images/figures/lincoln_styled_blockquote](https://ws1.sinaimg.cn/large/006tNc79gy1fm65qhxce7j30vj0ntgwa.jpg)

Figure 63: Styling a famous quote from an American president.

### [4.6Navigation styling](https://www.learnenough.com/html-tutorial#sec-navigation_styling)

As a final change to our sample website, we’ll make a change across all three pages by adding styling to the navigation menu added in [Section 3.5](https://www.learnenough.com/html-tutorial#sec-a_navigation_menu). In the process, we’ll yet again feel the pain of having to make the same change in several places, further preparing us to appreciate the value of the template system developed in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial).

To style the nav menu, we’ll first move it from the top left of the page to the more conventional top right. This will involve adding a style rule to the `div` tag that wraps the whole menu ([Listing 34](https://www.learnenough.com/html-tutorial#code-index_menu)). At the same time, we’ll add a left margin to the second and third nav links in order to improve the spacing. The changes to the book report page appear in [Listing 46](https://www.learnenough.com/html-tutorial#code-moby_dick_styled_nav), and the result appears in [Figure 64](https://www.learnenough.com/html-tutorial#fig-moby_dick_styled_nav).

Listing 46: Styling the navigation menu on the book report page.`moby_dick.html`

```
    .
    .
    .
    <div style="text-align: right;">
      <a href="index.html">Home</a>
      <a href="tags.html" style="margin: 0 0 0 10px;">HTML Tags</a>
      <a href="moby_dick.html" style="margin: 0 0 0 10px;">Moby Dick</a>
    </div>
    .
    .
    .

```

![images/figures/moby_dick_styled_nav](https://ws3.sinaimg.cn/large/006tNc79gy1fm65qw1dd0j30vj0nt7ff.jpg)

Figure 64: The styled navigation on the book report page.

Of course, we’re not done yet, as we need to make the same edits to the nav menu on the Home page ([Listing 47](https://www.learnenough.com/html-tutorial#code-home_styled_nav)) and HTML tags page ([Listing 48](https://www.learnenough.com/html-tutorial#code-tags_styled_nav)).

Listing 47: Styling the navigation menu on the Home page.`index.html`

```
    .
    .
    .
    <div style="text-align: right;">
      <a href="index.html">Home</a>
      <a href="tags.html" style="margin: 0 0 0 10px;">HTML Tags</a>
      <a href="moby_dick.html" style="margin: 0 0 0 10px;">Moby Dick</a>
    </div>
    .
    .
    .

```

Listing 48: Styling the navigation menu on the HTML tags page.`tags.html`

```
    .
    .
    .
    <div style="text-align: right;">
      <a href="index.html">Home</a>
      <a href="tags.html" style="margin: 0 0 0 10px;">HTML Tags</a>
      <a href="moby_dick.html" style="margin: 0 0 0 10px;">Moby Dick</a>
    </div>
    .
    .
    .

```

The results on the nav menu are exactly the same as shown in [Figure 64](https://www.learnenough.com/html-tutorial#fig-moby_dick_styled_nav). This is not surprising given that the changes represented by [Listing 46](https://www.learnenough.com/html-tutorial#code-moby_dick_styled_nav), [Listing 47](https://www.learnenough.com/html-tutorial#code-home_styled_nav), and [Listing 48](https://www.learnenough.com/html-tutorial#code-tags_styled_nav)are *all identical*. This sort of repetition is cumbersome and error-prone—definitely a [Bad Thing](http://www.catb.org/jargon/html/B/Bad-Thing.html). As mentioned several times before, we’ll solve this problem with a templating system in [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial).

#### [Exercises](https://www.learnenough.com/html-tutorial#sec-exercises_navigation_styling)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Change `margin: 0 0 0 10px;` to `margin-left: 10px` in [Listing 48](https://www.learnenough.com/html-tutorial#code-tags_styled_nav). What if anything changes in the appearance?
2. It’s conventional for navigation links not to change color after being followed, and they also look better if they’re not underlined like normal links. Using your Google-fu and the [w3schools](http://www.w3schools.com/cssref/) reference, guess the style rules for making these changes, and apply them to each element in the menu. *Hint*: The property you’ll have to modify to remove underlining is `text-decoration`. The result should look something like [Figure 65](https://www.learnenough.com/html-tutorial#fig-styled_menu).
3. Add a new table for the “document tags” that define the properties of the document. Include `html`, `head`, `body`, `title`, and `meta`.
4. Add any missing tags to `tags.html`. (By my count there are five after including the tags from the previous exercise.)

![images/figures/styled_menu](https://ws2.sinaimg.cn/large/006tNc79gy1fm65rcc6rjj30vj0nt4fq.jpg)

Figure 65: Styling the menu links.

## [5Conclusion](https://www.learnenough.com/html-tutorial#sec-conclusion)

Congratulations! You know know enough HTML to be *dangerous*. All that’s left is to commit and deploy the final sample website:

```
$ git commit -am "Finish the sample website"
$ git push

```

The result is a full website running in a production environment ([Figure 66](https://www.learnenough.com/html-tutorial#fig-deployed_website)). For reference, summary tables of all the block-level tags and inline tags appear in [Table 1](https://www.learnenough.com/html-tutorial#table-block_tags) and [Table 2](https://www.learnenough.com/html-tutorial#table-inline_tags), respectively.

![images/figures/deployed_website](https://ws4.sinaimg.cn/large/006tNc79gy1fm65rrifwij30vj0nt7g3.jpg)

Figure 66: A production website.

| **Tag**      | **Name**        | **Purpose**                              |
| ------------ | --------------- | ---------------------------------------- |
| `h1`–`h6`    | headings        | include a heading (levels 1–6)           |
| `p`          | paragraph       | include a paragraph of text              |
| `table`      | table           | include a table                          |
| `tr`         | table row       | include a row of data                    |
| `th`         | table header    | make a table header                      |
| `td`         | table data      | include a table data cell                |
| `div`        | division        | define block-level section in document   |
| `header`     | header          | label the page header                    |
| `ol`         | ordered list    | list elements in numerical order         |
| `ul`         | unordered list  | list elements whose order doesn’t matter |
| `li`         | list item       | include a list item (ordered or unordered) |
| `blockquote` | block quotation | show formatted quotation                 |
| `br`         | break           | enter line break                         |

Table 1: The block-level tags covered in this tutorial.

| **Tag**  | **Name**   | **Purpose**                       | **Example**                              | **Result**                               |
| -------- | ---------- | --------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `em`     | emphasized | make emphasized text              | `<em>technical sophistication</em>`      | *technical sophistication*               |
| `strong` | strong     | make strong text                  | `<strong>at least a billion people</strong>` | **at least a billion people**            |
| `a`      | anchor     | make hyperlink                    | `<a href="#"> Learn Enough</a>`          | [Learn Enough](http://learnenough.com/)  |
| `img`    | image      | include an image                  | `<img src="mhartl.jpg" alt="Michael Hartl">` | ![mhartl_gravatar](https://ws1.sinaimg.cn/large/006tNc79gy1fm65rwfzf1j301e01et8h.jpg) |
| `code`   | code       | format as source code             | `<code>table</code>`                     | `table`                                  |
| `span`   | span       | define inline section in document | `<span>Call me Ishmael.</span>`          | Call me Ishmael.                         |

Table 2: The inline tags covered in this tutorial.

At this point, you’ve got a solid foundation in the basics of HTML. To learn how to make industrial-strength websites, though, you’ll need to take the one additional step of reading [*Learn Enough CSS & Layout to Be Dangerous*](http://learnenough.com/css-and-layout-tutorial). And if you *really* want to take things as far as they can go, we recommend the full Learn Enough sequence:

1. Developer Fundamentals
   1. [*Learn Enough Command Line to Be Dangerous*](http://www.learnenough.com/command-line-tutorial)
   2. [*Learn Enough Text Editor to Be Dangerous*](http://www.learnenough.com/text-editor-tutorial)
   3. [*Learn Enough Git to Be Dangerous*](http://www.learnenough.com/git-tutorial)
2. Web Basics
   1. [*Learn Enough HTML to Be Dangerous*](http://www.learnenough.com/html-tutorial) (you are here)
   2. [*Learn Enough CSS & Layout to Be Dangerous*](http://www.learnenough.com/css-and-layout-tutorial)
   3. [*Learn Enough JavaScript to Be Dangerous*](http://www.learnenough.com/javascript-tutorial)
3. Intro Ruby Web Development
   1. [*Learn Enough Ruby to Be Dangerous*](http://www.learnenough.com/ruby-tutorial)
   2. [*Learn Enough Sinatra to Be Dangerous*](http://www.learnenough.com/sinatra-tutorial)
   3. [*Learn Enough Ruby on Rails to Be Dangerous*](http://www.learnenough.com/ruby-on-rails-tutorial)
4. Professional Ruby Web Development
   - [*The Ruby on Rails Tutorial*](http://www.railstutorial.org/)

Good luck!

*Learn Enough HTML to Be Dangerous*. Copyright © 2016 by Michael Hartl and Lee Donahoe.
