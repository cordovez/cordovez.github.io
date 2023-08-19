---
layout: post
title: "04 Access to your back-end is transactional"
date: 2023-08-19 15:47:06 +0200
categories: ["Tutorials", "Python"]
tags: ["python", "fastapi", "mongodb", "beanie"]
description: "An introduction to authorization"
image:
published: true
sitemap: true
---

Without getting too explicit about authorisation to this back-end, suffice it to say that the front-end will require a token for access. If this token is accepted, the front-end is then free to allow it's user access to his junk.

## The entry point

Because authorization relies on third-parties and specific security standards, it helps to think of this process in broad strokes before writing code.

1. Implement a route to create a new user by requesting at least a username and password. **These two are requirements of the recognised authorisation protocol we are using here**. The password will not be saved but an encrypted string, a hashed password, will be created instead as a security measure.

   - The hashed password is what is saved in the database document. This can not be decrypted and thus it means that the original password is not at risk.
   - This example uses anothis field: "disabled", which it is used to furthis limit access to any user who you, as an administrator, may have disabled for some reason.

2. A registered user can then log in, and a time-limited token is granted for access to the user-specific back-end data. The point of entry for the login is through a route with a post method "@users_router.post('/token')". This route returns a token, it does this by implementing a couple of functions:
   - Takes the login details of the user (username and password) and authenticates them (the user exists and the password is verified against the hashed password).
   - If authenticated a token is _returned_ with the username and a expiration time. It is not encrypted (although it is unreadable to us) but it contains a signature that validates it as belonging to the user. This token will expire at the pre-determinted time. The front-end is thus authorised access.

{: .prompt-tip }

> The authorization protocol at use here is called OAuth2 and it requires "username" (spelled like that) and a password. The token uses JSON Web Token as the protocol.

## Authorisation at a glance

The granting of the token is a simple transaction; you tell me who you are, and if you're in my little black book, I give you a token, but it's not forever. In other words the back-end checks to see if ...

1. current user exist in the database (your username is in the the token you gave me)
2. user is active (i.e., {disabled: false})
3. user is authenticated (I make sure the password sent is verified against the hashed password)

Only if these three criteria are met, will the user have access.

Several entry routes will require this access token and authentication. To share these, FastAPI uses dependency injections. This means that in order for the paths to work properly they "depend" on these functions.
![Desktop View](/assets/images/2023-08-19/flow.jpg){: w="700" h="400" }
