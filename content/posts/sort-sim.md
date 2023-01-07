---
title: "Sorting Algorithm Simulator 🌀"
date: 2022-01-22T12:22:38-05:00
draft: true
desc: "Test Description"
tags:
  [
    "algorithms",
    "javascript",
    "canvas",
    "sorting",
    "webworker",
    "comlink",
    "tones",
    "render",
    "web audio",
  ]
categories: ["projects"]
series: ["Themes Guide"]
ShowToc: true
TocOpen: false
---

In my journey to finally understand Data Structures & Algorithms (for real this time) I decided to document while I create my own implimentation of a sorting algorithm simulator.

#### **_Sorting algorithm [ASMR](https://www.youtube.com/results?search_query=sorting+algorithm+asmr) has entered the chat_**.

Thanks and credit to [sort.bullinger.dev](sort.bullinger.dev) which directly inspred this project.

I tried at first to create this on my own with no outside reference. Then I read through the inspiration source code and my mind was blown.

There was a lot going on. Web Workers. Typescript. New Web APIs. Smart, lean code doing it's job beautifully. It was beautiful.

I decided to take the long road on my way to DS&A mastery, and here's some of what I learned.

## The Plan 👻

Light, readable, vanilla JS/HTMl/CSS 🤤

- Accepts some user input on

  - the size of the array to sort,
  - the type of sort,
  - the number of operations per second.

- A pretty and minimal UI that visualizes the sort with audio feedback.

- Study the source code and understand each part. Understand the concepts beyond their usage here, and really get a grasp on some of the fundamentals of web development that they work with, beyond just rendering a

## Day One

1. **Make this blog and research 🔬**

I started by setting up this domain with GitHub Pages, updated the CNAME and A records with Google, enabled HTTPS, and started to explore some of the challenges I anticiapted for the task ahead.

This site is made with Hugo, the theme is PapaerMod, and the repo has a custom GitHub action to build and deploy on push to master. Neat!

Now onto the project.

I was most unsure about music playback, specifically browser generated tones.

✅ console.beep()

❌ /public/beep47.wav

I was curious about timing the audio and visuals together. Something something lifecycle.

I wanted to avoid relying on 100 different frequency .wav files and react bloat...

_Enter: new-to-me vanilla MDN Web APIs, [Canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) 🎨 and [Web Audio](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) 🔊._

2. **don't-create-react-app**

Next, I resist my zombie urge to make everything a react app 🧟‍♀️

There has got to be a leaner, meaner, and more fighting way forward.

After trying to take a whack at it on my own, I realized that this wasn't going to be the walk in the park I thought it was.
_Enter: ✨`<canvas></canvas>`✨_

I leanred that the four ways to draw things on the web are: Canvas, SVG, CSS, and direct DOM animation.

Recognizing that Canvas would use less memory and provide more control than the alternatives, it makes sense here.

I continued on with anything I could do that didn't involve actually learning more about sorting algorithms. Whats the hex-code for lightblue, I wonder.

3. **Learn about Canvas**

🥇 [Canvas Deep Dive](https://bucephalus.org/text/CanvasHandbook/CanvasHandbook.html)

🥈 [The HTML5 Canvas Handbook](https://bucephalus.org/text/CanvasHandbook/CanvasHandbook.html)

Two interesting and thorough resources for learning more about this whole canvas thing!

These Web APIs could honeslty be a post of their own [ future idea? ].

I ended today with some preliminary learning / trial and error about different ways to make a website beep, but that is a topic for tomorrow.

## Day Two

1. **So whats up, Canvas? 👨‍🎨**

_Enter: `CanvasRenderingContext2D.fillRect()`_ 💅👁👄👁💅

From MDN [herself](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/fillRect):

> The CanvasRenderingContext2D.fillRect() method of the Canvas 2D API draws a rectangle that is filled according to the current fillStyle.

`void ctx.fillRect(x, y, width, height);`

We can draw something, but how can we style it?

`ctx.fillStyle = color / gradient / pattern;`

Okay! We can work with this. We wanto to fill our 2d canvas, right?

![sort sim screenshot](/sortsim1.png)

Now we are getting somewhere.

2. **Web Worker API**

I mean... 👰

> Web Workers makes it possible to run a script operation in a background thread separate from the main execution thread of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.

🔑

> Service Workers essentially act as proxy servers that sit between web applications, the browser, and the network (when available). They are intended, among other things, to enable the creation of effective offline experiences, intercept network requests and take appropriate action based on whether the network is available, and update assets residing on the server. They will also allow access to push notifications and background sync APIs.

Okay, so that's all nice, but how does this help us with sorting?

Next, let's take a look at [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

This project is taking me down a a rabbit hole that's a little bit deeper than I had planned for this weekend, but that's okay and we are going to keep going.

> The Proxy object enables you to create a proxy for another object, which can intercept and redefine fundamental operations for that object.

> A Proxy is created with two parameters:
>
> target: the original object which you want to proxy
>
> handler: an object that defines which operations will be intercepted and how to redefine intercepted operations.
