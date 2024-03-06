---
layout: default
title: Branching
---

Just like last time, lets try and see what `git status` returns to us. 

And just like the last time, the staging area has not changed. As you may have guessed, this is also part of `git commit -m message` command. Lets fix this.

## Create a branch

Currently git does not know what to look for, because when we made our HEAD object, we made a pointer to branch `main`. However we never made a main branch, so the git does not know where to find the branch HEAD is pointing to. 

Each branch is saved as a file with hash-id of a commit object, so lets copy the hash of your commit object and make our first branch from scratch:

```
echo copyyourcommitobjecthash > .git/refs/heads/main
```

Now `git status` is happy and this is what my `.git` folder looks like:
```
.git
├── HEAD
├── index
├── objects
│   ├── 35
│   │   └── d7a9a460c597c8a29b210b2bed894a5281088e
│   ├── 79
│   │   └── e1fd1b22c75a812e59672d973cae307c036ef3
│   └── 86
│       └── 046e36f9b11251cf800033cec1c524502a6ce4
└── refs
    └── heads
        └── main
```

## Git log 

Lets take a look at command `git log` in our terminal:

```
commit 79e1fd1b22c75a812e59672d973cae307c036ef3 (HEAD -> main)
Author: Yijun2 <yijun@staut.land>
Date:   Wed Feb 28 12:07:20 2024 +0100

    initial commit
```

Now you are likely familiar with, or at least have seen, the output of `git log` before. The git log command begins its process by locating the HEAD, which searches for the hash ID `79e1fd1b22c75a812e59672d973cae307c036ef3`. Upon finding this hash, it fetches the commit information from the corresponding commit object we've recently created.

## Lets make a new branch
Creating a branch in Git typically involves using a high-level command like `git branch new-branch` So let's revisist our understanding of what a branch in Git represents. Based on what we've learned, a branch is essentially a reference (or a hash) to a commit object within the `.git` directory.

Now lets try to make a new branch from scratch called `dev` that pointing to the same commit as main branch, this time try to achive this without any guidelines.

When you are ready, you can verify with command `git branch` & `git log`, it should show both master and dev.

## Checking out the branch
As you probly noticed, we are currently on `master` branch. Lets try to checkout the new `dev` branch we just made and verify with command `git branch` or `git log`.
