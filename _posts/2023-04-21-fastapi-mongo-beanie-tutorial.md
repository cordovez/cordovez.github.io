---
title: "00 FastAPI, MongoDB, Cloudinary : An Introduction"
date: 2023-04-21 15:09:49 +0200
categories: ["Tutorials", "Python"]
tags: ["python", "fastapi", "mongodb", "beanie"]
description: "a more complex tutorial for beginners, where errors will be plenty"
image:
  path: /assets/images/JungleUrbanus.jpeg
published: true
sitemap: false
---

If you are like me, you have flitted from tutorial to tutorial in an effort to master Python and then attempted to finish a project only to realise that, while the tutorial exercise worked perfectly, your use case is different and you don't know how to solve the million errors that prop up when you go solo.

The problem with these tutorials is that they are simplistic. Yes, they teach you the basics in a clear and concise manner, but they are often a long way from a usable model that can be scaled up by replicating the code. That is because clarity and brevity are favoured over a project that would more closely resemble a “real-world” project.

Recently (weeks ago!) I (re)started a back-end project which I had previously done in NodeJS and now I want to perfect it in Python. Emboldened by my success after following several YouTube tutorials, I started from scratch and have found myself drowning in a million questions and errors. Today, I think I reached a point that while not complete or perfect, it is advanced enough that I can start writing about it and sharing what I have learned.

Realistically, most projects will have more than one simple "User" model as is the case in many tutorials. So I wanted to share my project that while basic, it offers plenty of scope for mistakes and learning through the use of more complex logic and organisational acrobatics.

This is the first of a series.

## The Project

A web app (as a preliminary step for a future mobile application) to help plant aficionados manage house plants. At first it will be a basic personal “plants-tagram” which provides a foundation upon which more complex features can be added (soil type, fertilisation schedules, propagations, light exposure,messaging, sharing, etc). To manage and store images, we will be using Cloudinary.

FastAPI, MongoDB, Cloudinary are the workhorses of this project and taken individually they are easy to understand, but it can tricky to make them play with each other.

MongoDB : The Database
FastAPI : The Python web framework
Cloudinary : media management and delivery tool
Beanie : The Object-document mapper (ODM)
JWT : The authentication method

## The Set-up

I will go through the set-up in very broad terms, as I am interested more in showing you how all the elements work in tandem rather than their set-up.

### Create a project folder

create a new project directory and cd into it. I decided to call this project “Plantopia”. You can call it whatever you wish. Then create a virtual environment and activate it with the following commands.

```zsh
mkdir plantopia && cd $_
python3 -m venv .venv
source .venv/bin/activate
```

{: .prompt-tip }

> I always name my virtual environments “.venv”. It makes them invisible and I don't forget the name when I need to activate it.

At the root level of your project, create a file called `requirements.txt` and paste the following list:

```
fastapi
pymongo
python-dotenv
uvicorn
motor
beanie
passlib[bcrypt]
python-multipart
python-jose[cryptography]
cloudinary
```

{: file="plantopia/requirements.txt"}

then run and installation of all these with this command on the terminal: `pip install -r requirements.txt`

### Create a MongoDB Free Account

Go to [MongoDB](https://www.mongodb.com/) and sign up for a free account and set up your database. The nomenclature can be a little confusing. You will create an “organisation” which will have a database deployment, and you'll also have a “project”, which you should give it the name “plantopia” or whatever you chose to call your project.

### Create a Cloudinary Free Account

Go to [Cloudinary](https://cloudinary.com/) and sign up for a free account. At the very basic cloudinary offers you space for saving photos and delivering them to your project as needed. This saves you from storing all those image files on your limited MongoDB database storage space. But Cloudinary is much more than storage. It also offers AI capabilities and editing tools which edit your images or videos on the fly.

## Conclusion

We are ready to start developing. I prefer to think of all the parts of the project as silos. In this introductory part we:

- [x] Set up our project files (for FastAPI)
- [x] Set up MongoDB
- [x] Set up Cloudinary

Stay tuned for the next step, setting up the DB models and saving documents.
