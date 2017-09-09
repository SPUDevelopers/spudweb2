+++
title = "Contribute to the Website"
date = "2017-09-08T19:55:28-07:00"
author = "Michael Bryant"
hide_authorbox = false
disable_comments = true
draft = false
enable_toc = true
categories = ["Guides"]
alert = "Rather than recreate much of the documentation necessary for this process, this guide instead links to the official docs."
+++

Have something you want to share with the SPU Developers community, maybe a how-to guide, or a review of some cool program you found, or even outlining a program you wrote yourself? Something that would fit nicely on a website like this? Or maybe you found something odd on the site, some bug that needs to be fixed, and want to let us know.
<!--more-->

This website's source is [hosted on GitHub](https://github.com/SPUDevelopers/spudweb2), so it is easy to do all of the above.

# Issues And Suggestions

First of all, if you have a suggestion or a bug to report, let us know on the [GitHub issue tracker](https://github.com/SPUDevelopers/spudweb2/issues). This requires a GitHub account, which you can [register for free](https://github.com/join), if you don't already have one.

## Issues

If you're reporting a bug, please give sufficient details about what the bug is as well as how we can reproduce it. In particular, please include the following information:

- Your web browser, version, and operating system (Edge on Windows 10, Firefox 53 on Linux, Safari on macOS Sierra, etc.)
- What page you were on, if applicable. If it occurs on all pages, please specify that instead.
- If the bug only appears under certain conditions or after specific actions are taken, please specify those here
  - For instance, if toggling the mobile menu on and off five times makes the toggle disappear, you should tell us that it happens only after toggling the menu five times.

## Suggestions

If you're providing a suggestion on how to improve the site, such as new behavior, content, or something else that is not a bug, please provide the following instead:

- The suggestion itself
- Why we should implement it - i.e. why would it be useful?
- If applicable, how many people do you expect to use the new behavior?

{{% alert %}}
Because Hugo, the program we use to generate the website, separates themes from sites, some bugs and suggestions may not be able to be implemented by us. Bugs related to the theme should be directed there instead, and any features that do not apply solely to SPU Developers can be directed there as well. If you aren't sure how it applies, just send it to us.
{{% /alert %}}

# Content

If you want to contribute content to the website, the easiest method for us would be for you to [fork the repository](https://help.github.com/articles/fork-a-repo/), make your changes, and submit a [pull request](https://help.github.com/articles/creating-a-pull-request/). If the content would be a considerable amount of work, please contact us through [Slack](https://spudevelopers.slack.com) or in a [GitHub issue](https://github.com/SPUDevelopers/spudweb2/issues) with your idea before starting. If we can't include your content for some reason, we don't want you to have gone through that work for nothing!

Assuming you have received the go-ahead from a club leader to make your contribution, you'll want to set up a few things:

- Set up [Hugo](http://gohugo.io/overview/installing/) ([Windows-specific directions](http://gohugo.io/tutorials/installing-on-windows/))
- Set up a Git environment on your computer. For Windows and Mac, we recommend using the [GitHub Desktop](https://desktop.github.com) application.
- Familiarize yourself with using Hugo. Some helpful links in the Hugo docs (though you should explore some of the other pages, too!):
  - [Getting Started](http://gohugo.io/getting-started/)
  - [Usage](http://gohugo.io/getting-started/usage/)
  - [Front Matter](http://gohugo.io/content-management/front-matter/) (aka page metadata)
  - [Content Management](http://gohugo.io/content-management/)

That's a lot of content in a lot of links, so we'll wait here while you go through all of it.

You're done? Cool. Let's move on.

From here, we're assuming that you have Hugo and Git set up on your machine following the instructions linked above.

{{% alert %}}
**Note to Windows users:** All `git` commands should be run using the "Git bash" program, which is available when you install GitHub desktop or Git for Windows. All `hugo` commands can be run using Command Prompt.
{{% /alert %}}

## Forking and Cloning the Repository

Begin by signing in to GitHub and accessing the [GitHub repository](https://github.com/SPUDevelopers/spudweb2) for this site. Click the "Fork" button to fork the repository to your account, then clone it to your computer. You can do this through the GitHub desktop interface or using the following commands.

{{< highlight bash >}}
cd /path/to/save/project/in/
git clone --recursive https://github.com/SPUDevelopers/spudweb2
{{< /highlight >}}

Replace `/path/to/save/project/in/` with the location you want the project folder to be located in, e.g.:

  - Linux/Mac: `~/Documents/`
    - `~` signifies the current user's home directory in Mac and Linux systems
  - Windows: `C:/Users/Username/Documents/`
    - Replace `Username` with your username

**Also be sure to substitute the URL with the one for your forked version.**

## Loading the Local Hugo Site

Next, open your terminal emulator or Command Prompt and navigate to the root of the local version of the repository (examples using the above example directories):

 - Linux/Mac: `cd ~/Documents/spudweb2/`
 - Windows: `cd C:/Users/Username/Documents/spudweb2/`
 - If you cloned the repository through GitHub Desktop, the path you want may look something like `C:/Users/Username/Documents/"GitHub Desktop"/spudweb2/`

You are now at the root of the Hugo site. If you type `ls` (Linux/Mac) or `dir` (Windows), you should see something like this:

{{< highlight bash >}}
archetypes  config.toml       content      data    layouts  public
README.md   requirements.txt  runtime.txt  static  themes
{{< /highlight >}}

From here, run the command `hugo server`. You'll see some output like below:

```
Started building sites ...
Built site for language en:
0 of 1 draft rendered
0 future content
0 expired content
5 regular pages created
5 other pages created
0 non-page files copied
2 paginator pages created
0 tags created
0 categories created
total in 182 ms
Watching for changes in /home/linuxuser/Documents/spudweb2/{data,content,layouts,static,themes}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Open your favorite web browser and navigate to <http://localhost:1313/>. You should see... the home page of this website.

Wow.

If you feel like it, open up the file under `content/post/hello-world.md` and make some changes to it, then save it. Go back to the local tab and visit the [Hello, World!](http://localhost:1313/post/hello-world/) post.

## Creating New content

From the root of the local repository, you can create a new page of content using the `hugo new` command in your terminal/Command Prompt:

{{< highlight bash >}}
# Syntax is "hugo new" followed by a path relative to the content/ folder
# Don't forget the .md file extension!
hugo new post/hello-world-v2.md
{{< /highlight >}}

If the local repository is found at `~/Documents/spudweb2/`, the new file will be created under `~/Documents/spudweb2/content/post/hello-world-v2.md`.

### The Front Matter

Open the file in your favorite programming text editor (we like [Atom](https://atom.io)). You should see something like the following:

```
+++
date = "2017-04-26T14:16:19-07:00"
description = ""
disable_comments = false
draft = true
hide_authorbox = false
thumbnail = ""
title = "hello world v2"
+++
```

This is the page's [front matter](https://gohugo.io/content/front-matter/), or metadata. Some of the lines above are page variables used in the site's current theme and may not appear if we change to a new theme. Some notes about these variables:

- `draft`: When set to `true`, this page isn't generated by Hugo (because it's a draft). Remove the line or set it to `false` to have the page appear on the site.
- `title`: This is automatically generated by Hugo based on the file name. I like to keep the file names all lowercase, but this means manually capitalizing the words in this variable, i.e. `title = "Hello, World! v2"`
- `description`: This is the description of the page as will appear on search engines. Keep it short but descriptive.
- `date`: This is a particularly formatted time string, based on the moment you create the file. If you take more than a day to finish the page, modify this string to match the current date/time.
  - The string follows the format of (YEAR-MONTH-DAY)("T")(24-HOUR TIME)(TIME ZONE)
- `hide_authorbox` and `disable_comments` are features of the theme we use and can be ignored because we (currently) don't use comments and authorboxes don't appear unless an `author` has been specified.

{{% alert %}}
The theme we use comes with its own set of [front-matter variables](https://bluestnight.shadow53.com/docs/pages/) that provide some extra functionality to the page.
{{% /alert %}}

### The Page Content

Pages on Hugo sites are formatted using a syntax called Markdown. Markdown allows text to be readable whether the formatting has been processed or not. For reference, check out this very page [in Markdown](https://raw.githubusercontent.com/SPUDevelopers/spudweb2/master/content/guide/website/contributing.md). It's not always the prettiest, but it's *much* better than trying to read HTML.

If you aren't familiar with Markdown, take a moment to look at these guides to the [basic](https://www.markdownguide.org/basic-syntax) Markdown syntax. There are also non-standard extensions to the Markdown syntax. [Click here](https://github.com/russross/blackfriday#extensions) to view which extensions Hugo's markdown parser supports.

An example file...

```
+++
# Front matter here
+++

Here is some example content.
This will appear on the same line as the sentence above.

This will appear in its own paragraph.

Here is a [link](#) that goes nowhere. [This one](https://spudevelopers.club) takes you to our home page.

What follows is an image of a SPUD:

![Image of a SPUD](https://www.gardenharvestsupply.com/productcart/pc/catalog/Russet_Seed_Potato_T.jpg)
```

... and what it generates to:

>
> Here is some example content.
> This will appear on the same line as the sentence above.
>
> This will appear in its own paragraph.
>
> Here is a [link](#) that goes nowhere. [This one](https://spudevelopers.club) takes you to our home page.
>
> What follows is an image of a SPUD:
>
> ![Image of a SPUD](https://www.gardenharvestsupply.com/productcart/pc/catalog/Russet_Seed_Potato_T.jpg)

#### Shortcodes

Hugo also provides something called [shortcodes](https://gohugo.io/extras/shortcodes/) to further extend your ability to make web pages. Examples include the [`{{</* highlight */>}}`](https://gohugo.io/extras/shortcodes/#highlight), [`{{</* (rel)ref */>}}`](https://gohugo.io/extras/shortcodes/#ref-relref), and [`{{</* youtube */>}}`](https://gohugo.io/extras/shortcodes/#youtube) shortcodes.

For example:

```
{{</* highlight javascript */>}}
for (var i = 0; i < 10; i++) {
  console.log("This is a JavaScript for-loop");
}
{{</* /highlight */>}}
```

displays as

{{< highlight javascript >}}
for (var i = 0; i < 10; i++) {
  console.log("This is a JavaScript for-loop");
}
{{< /highlight >}}

Perhaps an example that doesn't involve syntax-highlighting code that syntax-highlights code?

The `ref` and `relref` shortcodes are useful for generating the URL to another page on the site by filename. For instance, using the [Hello, World!] post as an example:

```
[Click me!]({{</* ref "post/hello-world.md" */>}})
```

becomes: [Click me!]({{< ref "post/hello-world.md" >}})

{{% alert %}}
The theme we use comes with [its own shortcodes](https://bluestnight.shadow53.com/docs/shortcodes/) as well.
{{% /alert %}}

## Submitting Your Changes (Pull Request)

When you've made whatever changes you'd like to submit to the site, the next step is to commit your local changes and push them to your fork of the repository. Here are instructions for [committing](https://help.github.com/desktop/guides/contributing/committing-and-reviewing-changes-to-your-project/) changes in GitHub Desktop and [syncing](https://help.github.com/desktop/guides/contributing/syncing-your-branch/) with the server.

For people using command-line Git (or Git Bash on Windows!), the commands you want to use are `git add`, `git commit`, and `git push`, like so (using `hello-world-v2.md` as the example):

{{< highlight bash >}}
git add content/post/hello-world-v2.md
# Provides an inline commit message. Use just "git commit" to
# write a multiline message in a text editor.
git commit -m "Added a second hello world post"
git push origin master
{{< /highlight >}}

Once the changes have been pushed to your fork on GitHub, you can file a [pull request](https://help.github.com/articles/creating-a-pull-request/). If we think your submission is useful, we'll merge it and you'll see your handiwork on the website! If we think there needs to be some changes made before it can be included, we'll ask you to fix those before we can merge. And if, for some reason, we have no need for your changes, your pull request may be rejected.
