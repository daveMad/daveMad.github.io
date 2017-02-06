---
layout: post
title: How to Change Github Repository Language
categories: [Git]
tags: [git,notes]
---

## Github Linguist

It's a library used on Github to detect repository languages. You can check it out [here](https://github.com/github/linguist)

##  GitAttributes

We'll need a **.gitattributes** file in order to change the repo language. I'm using Windows, and it does not allow me to define a new file with name starting with a **dot**. If you are having such a case, you can type the following command from the command line:

`echo .> .gitattributes`

 or you can  just download [this sample](https://github.com/daveMad/daveMad.github.io/blob/master/.gitattributes) 

## Add a single line and it's done

Let's say you want your css code to be seen as a javascript code. In order to achieve this, just add the line below to **.gitattributes** file:

`*.css linguist-language=Javascript`

Add your changes, commit and push to your repository. Then on the main page of your repo, click on the **colorful bar** just below commits counter bar. You'll see your code's language percentages.