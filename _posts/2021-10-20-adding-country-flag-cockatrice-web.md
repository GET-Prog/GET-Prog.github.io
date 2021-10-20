---
layout: post
title:  Adding Country Flag to Cockatrice Web
date:   2021-10-20 19:00:00 -0300
author: Bruno Mendes
github: brnomendes
---

Hacktoberfest is an event organized by DigitalOcean, having its first held in [2014](https://www.digitalocean.com/blog/hacktoberfest/). At hacktoberfest, developers from around the world come together to make contributions to open source projects in the month of October. Typically these projects are located on [Github](https://github.com/) and other similar platforms. In addition to being fun to participate in the hacktoberfest, you contribute to the community and can win a DigitalOcean reward like a t-shirt.

Rules for participation can be found in [Hacktoberfest website](https://hacktoberfest.digitalocean.com/). This year, the authors of GETPro set themselves a challenge for the hacktoberfest: a coded contribution to a public open source repository containing more than 10 stars on Github. This post is to tell about my experience in this challenge.

The project I chose to contribute was [Cockatrice](https://cockatrice.github.io/), an application that lets you play card games virtually (like Magic: The Gathering :hugs:). Cockatrice is originally a desktop application written in `C++`, but they're developing a web version with React, and it's this web version that we're going to talk about in this post. You can see the desktop version in the image below:

![cockatrice-desktop](/assets/cockatrice-desktop.png)

As of this writing, Cockatrice's web client is still in the early stages of development so there's still a lot to do. In addition to having the `hacktoberfest` tag the repository has 1.1k stars, so it's good for our challenge!

Let's go to action. We initially cloned the repository using:

```
git clone git@github.com:Cockatrice/Cockatrice.git
```

Then, in the application path, as it's a node application, we install the dependencies with `npm i` and we can run it using `npm run start`.

When starting the application for the first time, what we saw was the following image.

![cockatrice-web](/assets/cockatrice-web.png)

The first thing that differs from the desktop version is that next to each user they don't have a flag indicating their country, so that was the point I intended to attack.

Exploring the code I saw that there was already an array with the images of the countries' flags:

```jsx
const Countries = [
  ...
  bq,
  br,
  bs,
  ...
]
```

So one thing I changed was so that this object could be accessed through a string (for example, `br` for Brazil):

```jsx
const Countries = {
  ...
  bq,
  br,
  bs,
  ...
}
```

Then, I went to the component where I should change it, so this already received the username:

```jsx
...
const { user } = this.props;
const { position } = this.state;
const { name } = user;
...
```

I also started to receive the country:

```jsx
...
const { user } = this.props;
const { position } = this.state;
const { name, country } = user;
...
```


The space to place the flag already existed in the code:

```jsx
...
<NavLink to={generatePath(RouteEnum.PLAYER, { name })} className="plain-link">
    <div className="user-display__details" onContextMenu={this.handleClick}>
    <div className="user-display__country"></div>
    <div className="user-display__name single-line-ellipsis">{name}</div>
    </div>
</NavLink>
...
```

I changed it from `div` to `image`:

```jsx
...
<NavLink to={generatePath(RouteEnum.PLAYER, { name })} className="plain-link">
    <div className="user-display__details" onContextMenu={this.handleClick}>
    <img className="user-display__country" src={Images.Countries[country]} alt={country}></img>
    <div className="user-display__name single-line-ellipsis">{name}</div>
    </div>
</NavLink>
...
```

And I set the size in the style file:

```css
.user-display__country {
  width: 1.1em;
}
```

Now we have the result below:

![cockatrice-without-magin](/assets/cockatrice-without-magin.png)

But the flag was very close to the username, so to finish I added a margin:

```css
.user-display__country {
  width: 1.1em;
  margin-right: 0.4em;
}
```

And we have the final result:

![cockatrice-flag](/assets/cockatrice-flag.png)

At the end, my pull request can be found at [Show country flag in user list of webclient](https://github.com/Cockatrice/Cockatrice/pull/4431). It was approved and merged by a maintainer approximately 1 hour after I opened it. I even received a "Well done! Good job on the switch to company map from array" compliment on my first pull request in this repository.

If you also want to participate, stay tuned at [Hacktoberfest website](https://hacktoberfest.digitalocean.com/) that every year in October you have this opportunity.
