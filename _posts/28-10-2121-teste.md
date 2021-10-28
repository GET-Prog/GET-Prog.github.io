---
layout: post
title:  Contributing to Open Source projects could be hard
date:   2021-10-20 19:00:00 -0300
author: Danilo Sambugaro
github: dsambugaro
---

So, in summary, I was trying to contribute to an open software project but get my pull request refused without any request for changes about it, but let's start from square one for better context.

So, if you don't know about the Hacktoberfest event, you probably should. Hacktoberfest is an event organized by DigitalOcean, that aims to encourage participation in the Open Source community. This event occurs every year since [2014](https://www.digitalocean.com/blog/hacktoberfest/) and if you beat the year's challenge you can win some rewards like a very nice and comfortable t-shirt and some stickers. More about this great event can be found at [Hacktoberfest website](https://hacktoberfest.digitalocean.com/).

Goin on, this year, the authors of GETPro set themselves a challenge for the Hacktoberfest: a coded contribution to a public Open Source repository containing more than 10 stars on Github and I'll talk about my experience in this challenge.

So the first step was to find a repository that match the requirements of the challenge. I find two good candidates and I was aiming to resolve one issue in each repository, but one of the issues I was hoping to resolve had been taken by another person before I could do it. That's ok, I still had another project to work with.

I choose to contribute to the repository [op-website-hugo](https://github.com/OsProgramadores/op-website-hugo), which basically is the website of the [OsProgramadores](https://osprogramadores.com) group. This is a Brazilian group to talk about programming and related topics. The repository, the commits, the comments, everything is in *pt-BR*.

The issue I was trying to resolve is the [#366](https://github.com/OsProgramadores/op-website-hugo/issues/366),  which requests the combination of two sections of the site, *Rules* and *FAQ*, to get more free space on the menu. Any other description wasn't given in the issue.

Here is the menu before I start my changes:
![op-hugo-before.png](/assets/op-hugo-before.png)

I thought that will be better to put these two sections under an only menu section, which I called `About`. So I made this section have a dropdown menu with links for the Rules section and the FAQ section.

Here is the menu after I start my changes:
![op-hugo-after.png](/assets/op-hugo-after.png)

With these changes up and working, I made my [pull request](https://github.com/OsProgramadores/op-website-hugo/pull/592) to the repository. About one day after I open my request, one of the maintainers (the same who opened the issue) closed my pull request with the comment:

"Thanks for the suggestion but I think it's ok as it is now.
People don't even look at the rules they are on the first level of the menu. If you put it down there, no one will look at it at all.", in free translation.

Ok, I totally agree with what he said here, it's a polite answer and objective. And if I was proposing a new thing that doesn't have an issue related to it, that will be a good answer I think. but the case here is that we have an issue and I was trying to make a contribution to solving the case. I think that the maintainer could be more comprehensive on that point. I think that one of the hardest things in entering the Open Source contribution, besides the fact that you'll maybe be handling a totally new project or technology that you'll have to understend, is the fact that the software maintainers maybe not know how to behave with a new and unexpected contribution, maybe they just disapprove it without giving you the chance to improve what you have made.

I think that in that case he could be explained that isn't what they want, how he did, but also explain how he was imagining the solution for that issue, he could have asked for specific changes or opened a discussion about how we could find a better solution, I don't know. BUT, to be fair, when I have chosen the issue I could open a discussion about it, asking how they want it to be made, if they had any ideas about it.

So, in my point of view, both sides made mistakes, something that I'll keep with myself to improve my next contributions to the Open Source community.
