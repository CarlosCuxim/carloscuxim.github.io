---
title: 'My adventure creating a blog'
published: 2025-08-17
draft: false
description: 'All the process to create this blog and the tools for that prupose.'
tags: ['tutorial']
---

Well, this should be the first entry of my blog. For a while now I had been
planning to create a blog just to capture all the ideas that come to my mind.

The problem wasn't so much creating it, there are many ways. The original idea
was simply to use a Python script to convert markdown files into html files
with a predefined template. Another option was just to use pure HTML (in fact,
I already had something like that, but it didn't last long). The biggest
problem wasn't programming it, but that every time I wanted something new,
like including math, a tag to write code, a default CSS style, etc., I had to
stop writing the blog entry, make the changes, and finally continue writing.
This made a simple entry take hours.

In the end I got fed up. But while continuing to search I saw that there are
static HTML generators, where it's enough to write a `.md` and it generates a
site with the respective links. It's practically what I wanted to do with the
Python script. And well, I'm one of those who think it's not necessary to
reinvent the wheel (unless that's what you want).

With the plan of using a static site generator, there were two questions I had
to resolve. The first is: Where will the site be stored? In other words, what
should be the host? I had two options. The first was to use the VPS I'm
currently renting and use the [domain I'm renting](https://cuxim.com).
This isn't a bad option, I hardly have processes on the VPS so it wouldn't be
a bad use. Although it's not very complex, I would still have to configure
the ports, SSL certificates, and the way to deploy (since the VPS is in
Europe the ping is bad enough editing through ssh feels like torture).

So what I decided was simply to take advantage of GitHub Pages which does all
that process for me. I just need to clone the repository, push, and that's it,
it should be working.

The problem comes with the second question I had to resolve: Which site
generator to use? The initial plan was to use Jekyll, it comes native with
GitHub and there are several tutorials for it. Not a bad option, but I decided
to look for other options. In fact, depending on the option I chose, I would
have to discard the possibility of using GitHub Pages. However, to my surprise
GitHub has a better way to generate its pages besides the native Jekyll one,
and that is through [GitHub Actions](https://docs.github.com/en/actions).
The truth is I don't really understand how it works, I tried reading the
documentation, but my reading comprehension (at an elementary school level)
didn't make it clear what I had to do.

On Reddit forums I saw the different options offered by GitHub Actions, of
which three seemed interesting: Jekyll because it's the simplest way, Hugo
which looks quite fast and practical, and finally Astro. I leaned towards the
latter since it seems to have the most customization available, plus it has a
[specific tutorial for GitHub Pages](https://docs.astro.build/en/guides/deploy/github/).

This is the point I'm at right now. The goal of this first entry is simply to
narrate all the steps I'm following so this blog works at least with this one
entry. For more context, I'm working on a laptop with pretty precarious specs
(an Intel Celeron with 4 GB of RAM) in a (almost) new installation of Arch
Linux. This isn't an operating system I usually work with often, but nothing
is learned through comfort.

The first problem I'm noticing is that the tutorial assumes you already have
an Astro project, so I have to go back to the tutorial on how to install and
use it. First there's the
[installation tutorial](https://docs.astro.build/en/install-and-setup/).

The installation was relatively quick, just using `npm` and following the
installer instructions. Well, or at least that's what I thought, because when
I tried to run the command `npm run dev` the following message appeared:

```log
> carloscuxim-github-io@0.0.1 dev
> astro dev

sh: line 1: astro: command not found
```

Of course not everything could go well. I think it's an unwritten rule of
programming (and mathematics) that if something seems to be going too well,
it'll probably break at some point.

The issue is that the message makes me suspect that some program is missing
for installation. I mean, it's pretty clear it indicates that the `astro`
command is trying to execute but the shell can't find it. Well, after a while
searching on Google what was happening, I found several solutions. First,
install astro globally with `npm`, which isn't a bad solution, but with node
I prefer not to install anything globally, mostly because one of interesting
things about node is that it allows you to have a 'virtual environment' where
everything is well packaged and without external dependencies. The second
option was to install it locally and change the `run` script so it runs
through `npx`, also not a bad option, but I don't know if other parts of the
documentation assume astro was installed globally, so that's my last option
Fortunately the solution was dumber than I thought, it was simply rerunning
`npm install`. I don't know if something didn't install correctly using the
creation wizard, but well, in the end it's a note to keep in mind that maybe
necessary to reinstall the dependencies.

Well, after a while reading the documentation I think I made a big mistake,
it's not beginner friendly at all. It seems to use a component structure
similar to React or Vue.js. Honestly I'm not sure where everything is. But seems I have a second chance. Apparently there's a tutorial focused on
[creating a blog](https://docs.astro.build/en/tutorial/0-introduction/),
maybe there I can get a good starting point if I want something more advanced.

I think I'm getting the hang of it. When you create a project in astro you get
a folder called `src/pages` where each of the pages to be rendered are. The
root page is saved in `index.astro` and the components just have to be
imported from the other folders, which is quite simple. Although for now it's
very similar to writing `html` using a framework, I'd like it to just take a
markdown as input, but I'll go step by step. The tutorial first indicates you
have to upload it online. I get that it's a tutorial aimed at new people, but
since in my case I want to upload it to GitHub Pages, I'll have to step a bit
away from the tutorial.

Well, in fact making GitHub process the page was much simpler than I thought.
You just have to add the instructions in the file
`.github/workflows/deploy.yaml`. For now I'm using the instructions offered in
the [Astro tutorial](https://docs.astro.build/en/guides/deploy/github/), so
it was quite simple. I guess if I require a more advanced process things will
change, but for now it works and that's all I ask for. With this I can continue with the tutorial to create a blog.

Well, a few hours have passed reading the tutorial and the documentation. And
I've learned one thing: this is HTML with extra steps. It lets you organize
things quite well with components, but it's not really for creating a blog.
This doesn't mean you can't, not at all, just that it's not its only purpose.
Astro is a pretty advanced system to be able to create static pages, it's
similar to React but not so focused on JavaScript, more focused on HTML.

The point is that my purpose in using a static site generator isn't so much to
have a fully attractive blog, but to have a functional blog where I can focus
only on writing entries without fighting so much with the internal workings of
the page. Am I going to change astro? Not at all, astro is quite interesting
and I feel I can create very interesting things with all the tools it gives.
But at the same time I need something that simplifies my life.

With this goal, searching (and asking ChatGPT if I'm honest) I came across
[Astro Themes](https://astro.build/themes/). On this page you can find many
templates to use. Some are paid, but others are free. In my case, after
searching hard through the first page of results, I decided on the
[multiterm-astro](https://github.com/stelcodes/multiterm-astro) theme which
makes the blog look like a command console.

The installation was simple, just fork it and use the already established
structure. There are still things I want to modify, like the font when code is
rendered. However, for an adventure that took me a whole day, I think it's
enough.

Ultimately, this will be a process of trial and error. I just hope this first
post won't be the only one here.
