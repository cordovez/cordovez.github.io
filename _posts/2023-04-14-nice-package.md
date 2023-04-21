---
layout: post
title: Nice package init?
date: 2023-04-14 13:04:08 +0200
categories: [Python]
tags: [python, beginners]
description: Why we need to use '__init.py__' in our Python projects and importing paths.
image:
published: false
sitemap: false
---

When I took my first steps in starting a Python project solo, I ran into difficulties importing files and modules. I had cloned someone's project and I wasn't yet familiar with the way Python imports worked, so I assumed it had something to do with those strange files in each folder labelled "\_\_init\_\_.py"

After reading _Python Distilled_ by David M. Beazly, I now understand not only why they are important to use, but also what happens when you don't.

## Packages

In short, assuming that you are creating a project in a named folder, which in itself has other folders within it to separate your code in an organised and logical manner, then the _init_ file helps import the modules/files contained in your project relative to their position in the project hierarchy. The "\_\_init\_\_.py" file is necessary for distributing your project, so it is good practice to include it.

However, you may have realised that you can indeed import from one module to the other without the use of the init file. But by doing this, you are creating a more advanced hierarchy of files used mainly for large and complex enterprise-level projects where the code needs to be separated into separate packages.

Another way to think about it is that by using "\_\_init\_\_.py" you are creating a "package of modules" and without it you are creating a "package of packages" called _namespace package_.

## Importing within a package

When I want to launch a project for coding in VS Code, I type in my terminal "code ." but in my head I read it as "code this".

I use the same logic when referring to import notation inside a package.
![Structure of a package](/assets/images/init_structure/init_structure.001.jpeg){: .light}
![Structure of a package](/assets/images/init_structure/init_structure.002.jpeg){: .dark}

text
