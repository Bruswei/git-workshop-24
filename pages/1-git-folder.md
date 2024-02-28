---
layout: default
title: Create .git
---

Welcome to our workshop's journey into Git's inner workings! Normally, when we start versioning changes in our projects, we rely on commands like `git add` and `git commit` to track our modifications. However, to truly grasp the magic behind how Git saves and manages these changes, we're going to dive deeper and take a hands-on approach, doing it all manually, without relying on those commands. 

### Create a New Folder for Your Repository

Begin by creating a new folder on your computer. This folder will serve as your local repository.

### Create a .git Folder

Normally we would use command `git init` to set up repository and funcionalities locally, but for the learning purpose, we are going to setup a `.git` folder from scratch. 

Lets make a git folder by using command `mkdir .git`, and it should now create an empty `.git` folder for us that can serves as "database".


### Lets verify our git repository

Lets verify if this works as intended, run `git status`. 

If you see `fatal: not a git repository (or any of the parent directories): .git`, don't worry. Lets see what's the problem here.

As we mentioned earlier, in our "git database" there will always contain:

- A collection of objects

- A system for naming those objects

Ok, lets make these from scrath.


### Lets fix our git database

Objects such as Blobs, Trees and Commits are stored under a folder called `objects`.

References or many of us calls it for branches are stored under `.git/refs/heads`.

Let's make the folders and verify if it works now.

```
mkdir .git/objects
mkdir .git/refs/heads
git status
```

Not quite yet, because when we are running `git status`, git is trying to figuring out our current repo or status of the project. But since we do not have naming or objects available in the database, git is looking for `HEAD` but it is not available currently. 

So lets make a `HEAD` and verify:

```
echo ref: refs/heads/main > .git/HEAD
git status
```

Now git status thinks that we are on branch `main` and we kinda achive what we are aiming for here.


<footer style="width: 100%; display: flex; justify-content: space-between; padding: 20px 0;">
    <a href="../index.html" style="float: left; margin-left: 10px;">Previous Step: Setup</a>
    <a href="./2-blob.html" style="float: right; margin-right: 10px;">Next Step: Make a blob</a>
</footer>