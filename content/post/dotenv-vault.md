---
title: "Dotenv-vault, how to safely manage your envfiles in a collaborative environment"
date: 2022-09-23T11:30:02+00:00
# weight: 1
# aliases: ["/first"]
tags: ["dotenv","vault", "envfiles", "collaboration"]
author: "Gittre"
# author: ["Me", "You"] # multiple authors
draft: false
hidemeta: false
comments: true
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowWordCount: true
---

# Bootstrapping a project 
When bootstrapping a project many tasks like executing and building it require some variable to be set.
Those variables are usually stored inside a `.env` file and later supplied to those processes.

# Solving a security issue
`.env` files usually contain private or sensitive data, such as API Keys and other pieces of information that should never go public.
For this reason, `.env` files and application code are never shipped together, so we'll need to pass `.env` files around for security reasons. 
Ideally, we want them to be stored and encrypted in a safe place that we can access and give access to cause that would also make collaboration easier. 
For those purposes, we chose Dotenv-vault.


# Dotenv vault and how it works
Dotenv-vault can securely store `.env` files' data on a virtual vault and retrieve them whenever we want.
It also supports versioning and collaborative access options, but let's dive deeper into how it works.

## Setup and Workflow
First of all, we need to create a vault.
To do so, open up the terminal and cd to your project folder, then run:

 `npx dotenv-vault new`

npx will install Dotenv-vault if it doesn't exists and ask for vault initialization.

Once we initialized the vault, we'll need to login:

`npx dotenv-vault login`

It will open up a browser window and prompt for login.
After logging-in we can either:
- `npx dotenv-vault push` and store`.env` files data to the vault
- `npx dotenv-vault pull` and retrieve our data from the vault

Additionally, you may use `npx dotenv-vault open` to open a browser window containing your `.env` files and their data. Here you can also give other people access to the vault.

But let's see how all of this is made secure:
- Data is sent over an encrypted connection
- Data gets decrypted and held in memory for the storage process. Once data is re-encrypted and stored, memory gets flushed. Decrypted data never persists.
- Keys and values from the  `.env` file are encrypted with different keys and then saved in different places so, in case of breaches, it would be hard to make sense of the data. 

## Conclusion
Dotenv-vault is easy-to-learn, easy-to-use storage for your environment variables: designed with security in mind, it makes collaboration easy and versioning painless. 
We explored the basics, but you can learn more about it at https://www.dotenv.org.