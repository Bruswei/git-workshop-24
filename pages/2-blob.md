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
> You can also use `git cat-file -t 35d7a9` to see the type of the object. In this case, it should print out as a `blob`.

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


<footer style="width: 100%; display: flex; justify-content: space-between; padding: 20px 0;">
    <a href="./1-git-folder.html" style="float: left; margin-left: 10px;">Previous Step: .git folder</a>
    <a href="3-tree-commit.html" style="float: right; margin-right: 10px;">Next Step: Create a commit </a>
</footer>