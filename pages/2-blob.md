---
layout: default
title: Create Blobs 
---

Now that we have a functional git, lets see what happens if we run `git log `. 

It should have return some sort of error, since the branch HEAD is pointing to have no commits or exist. Now lets make our first commit and branch.

### Add a README File

Create a new file named `README.md` in your repository folder (not inside the `.git` folder). Open this file in a text editor and add the following content exactly:

```
This repository was made manually without git init!
```

Save and close the file.

### Create a Blob Object

A blob object in Git represents the contents of a file, and this is typically achive by `git add README.md`. To create a blob object, you will generate a hash based on the contents of your `README.md` file. 

Before we begin, lets take a look at the .git structure we have currently:

```
.git
├── HEAD
├── objects
└── refs
    └── heads
```

Do the following in terminal:

```
git hash-object README.md -w
```

Command `hash-object` is another plumbing command and it hashes an object for us, and with `-w` flag we are asking git to store it for us in `.git` folder. Lets see what happens with the `.git` now:

```
.git
├── HEAD
├── objects
│   └── 35
│       └── d7a9a460c597c8a29b210b2bed894a5281088e
└── refs
    └── heads
```

We have now received a new object, under `.git/objects`. It might looks weired at the first glance, but lets see what is the hash of the `README.md` file, this time we will run it without `-w` flag.

```
git hash-object README.md
```

It printed out `35d7a9a460c597c8a29b210b2bed894a5281088e`. So as we can see, git takes the first two characters and made it a folder before the rest is saved under it. 
 - By doing this way git increases the performance and efficiency when looking for another object. Many file systems are much faster with smaller directories than larger once, some of the file system even have limits.

Now, when we execute `git cat-file -p 35d7a9` or `git show 35d7a9`, it should display the content you've added to `README.md`. Assuming you have followed the instruction precisly, you should see: 
```
This repository was made manually without git init!
```
>> You can also use `git cat-file -t 35d7a9` to see the type of the object. In this case, it should print out as a `blob`.

**Note: Did you find it curious that the hash from your `README.md` file matches the one mentioned here before you even hashed it on your machine? That's Git's magic at work, utilizing SHA-1 hashing to create a checksum for the objects. If the hash in your `.git` folder matches the one here, it indicates that the files are indentical according to Git.**

## Update the index

As we mentioned earlier, we are making a blob manually in this workshop to replicate the step `git add README.md`, but lets see what happens when we run `git status` in the terminal.

Why isn't `README.md` stagged like when we run `git add README.md`? The pocelain command `git add` hashs the objects, structure and also update the `index` of the git. Sometimes we refering it as `Staging`. So lets do that with plumbing command `git update-index`:

```
git update-index --add --cacheinfo 100644 35d7a9a460c597c8a29b210b2bed894a5281088e README.md
```
_100644 is representing file permissions and not important for this workshop_

Now my `.git` folder looks like this:

```
.git
├── HEAD
├── index
├── objects
│   └── 35
│       └── d7a9a460c597c8a29b210b2bed894a5281088e
└── refs
    └── heads
```

We have gotten a new `index` file here. Now lets look at the our staging now with `git status`, you should see that now `README.md` is staged and ready for commit.

### Create a tree object

After creating a blob object for your `README.md` file, the next step is to create a tree object. A tree object in Git represents a directory and its contents, which could be other directories (sub-trees) or files (blobs). For our simple repository, the tree object will just contain the `README.md` blob and its name.

A tree object lists all blobs (files) and trees (directories) that reside in a directory. This is typically achive by command `git commit -m "commit message"`. 

Each entry in a tree object has a mode, type, SHA-1 hash, and name. Here's an example of what a tree object might look like:

```
100644 blob abc123456789... README.md
```

* 100644 is the file mode for a regular file.
* blob indicates that this entry is a file (blob).
* abc123456789... is the SHA-1 hash of the blob object for README.md.
* README.md is the name of the file.

[When you are ready, click here to start the creation of your first tree object.](create-tree-object.md) for a detailed steps. 

## Step 6: Create a Commit Object

<!-- A commit object records the state of your repository at a certain point in time. To create a commit object:

Write a commit message that describes the changes you are committing.
Include details such as the author, committer, and the timestamp.
Create a SHA-1 hash for the commit metadata and the tree object that records the directory structure of your project.
Store the commit object in the `.git/objects` directory. -->


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

After we have created blob and tree object, it is time to create a commit object from scratch! 

[Here is a detailed steps on how to do it](create-commit-object.md)

By the end of these steps, you will have manually created the initial commit for your repository.

<footer style="width: 100%; display: flex; justify-content: space-between; padding: 20px 0;">
    <a href="./1-git-folder.html" style="float: left; margin-left: 10px;">Previous Step: .git folder</a>
    <a href="3-tree-commit.html" style="float: right; margin-right: 10px;">Next Step: Create blob </a>
</footer>