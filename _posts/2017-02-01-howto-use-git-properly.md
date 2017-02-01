---
layout: post
title: How To Use Git Properly
categories: [Git]
tags: [git,productivity,notes]
---

## Git Matters a Lot

Dead simple, you don't lose your files, you can track your progress, use milestones, open issues, reviewing etc. on Github. Github powers Git a lot. These are very important stuff. When i started using Git, i was commiting big changes, then i realized that if possible, we gotta commit every time a file changes. I mean, if **README.md** changes, add a commit like this: 

```Bash
git commit -m "change readme.md"
```

If you're the only one use the repository, i accept that this usage seems like a waste of time, but if a big team uses this repository, commiting every change helps other to understand your code more easily.

## Pull Requests

Use on **cli** or Github's website, does not matter. Opening a pull-request is fairly easy, it should be, though. Using Travis to check your commits, discussing on the commits / changes and all that fun stuff makes collaboration easier.

## Github / hub cli

Did you hear about **hub cli**? It extends your git bash. Sometimes i don't even need to go to Github's site and do stuff. I can **fork my repository, open pull-Requests** from hub cli. Check it out [here](https://hub.github.com/) , if you are type of command line dude like me!

## Master Git by Free E-book

Go to original website git-scm.com. You should see a book named **Pro Git** there. It's free and you find the V2 by clicking this [link](https://git-scm.com/book/en/v2).