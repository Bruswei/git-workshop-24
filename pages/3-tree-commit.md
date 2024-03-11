---
layout: default
title: Create a commit
---

### Create a tree object

After creating a blob object for your `README.md` file, the next step is to create a tree object. A tree object in Git represents a directory and its contents, which could be other directories (sub-trees) or files (blobs). For our simple repository, the tree object will just contain the `README.md` blob and its name. When we use `git commit -m "commit message"`, it updates the tree objects from `index` file we just created.

Lets make our tree by running command:

```
git write-tree
```

Now our .git folder looks like following:

```
.git
├── HEAD
├── index
├── objects
│   ├── 35
│   │   └── d7a9a460c597c8a29b210b2bed894a5281088e
│   └── 86
│       └── 046e36f9b11251cf800033cec1c524502a6ce4
└── refs
    └── heads
```

A new object is now created under `.git/objects` and the hash was `86046e36f9b11251cf800033cec1c524502a6ce4`. We can verify with `git cat-file -t 86046e` and `git cat-file -p 86046e`.
> Flag -t stands for type and -p stands for print.

## Create a Commit Object

Lets have a sync and do a `git status`, and we should see the result is the same as last time. Same as `git add` the command `git commit -m message` performs several operations internally, and update tree structure is part of it. As you may have guessed, lets make a new commit object.

A commit object in Git encapsulates the state of a repository at a given point in time. It includes the following information:
* **Tree SHA-1:** The SHA-1 hash of the tree object that represents the directory structure of the commit.
* **Parent SHA-1:** The SHA-1 hash of the commit's parent(s). For the first commit, this field is absent.
* **Author:** The name, email of the author of the changes, and the timestamp.
* **Committer:** The name, email of the person who committed the changes, and the timestamp.
* **Commit Message:** A descriptive message explaining the commit.

Here's an example of what a commit object might look like (simplified):
```
tree 2f3a123456789...
author John Doe <john@example.com> 1625592667 -0400
committer John Doe <john@example.com> 1625592667 -0400

Initial commit
```

To achive this, we can use plumbing command:

```
git commit-tree 86046e36f9b11251cf800033cec1c524502a6ce4 -m "initial commit"
```

This is what `.git` looks like now:

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
```

You should have received a new object with a different hash than what shows above, this is because the content of the commit object is different, like autor and comitter.

Lets verify the new object with `git cat-file -t <hash-of-your-new-commit-object>` and `git cat-file -p <hash-of-your-new-commit-object>`



<footer style="width: 100%; display: flex; justify-content: space-between; padding: 20px 0;">
    <a href="./2-blob.html" style="float: left; margin-left: 10px;">Previous Step: Create blob</a>
    <a href="./4-branch.html" style="float: right; margin-right: 10px;">Next Step: Branching</a>
</footer>