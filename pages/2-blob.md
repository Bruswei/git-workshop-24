---
layout: default
title: Create first commit
---

### Step 3: Add a README File

Create a new file named `README.md` in your repository folder (not inside the `.git` folder). Open this file in a text editor and add the following content exactly:

```
This repository was made manually without git init!
```

Save and close the file.

### Step 4: Create a Blob Object

A blob object in Git represents the contents of a file, and this is typically achive by `git add README.md`. To create a blob object, you will generate a hash based on the contents of your `README.md` file. 

Generate the hash for the file contents prefixed with the necessary Git blob header. Save this hash as a file in the `.git/objects` directory, following the convention that Git uses for object storage.

[When you are ready, click here to start the creation of your first Blob object.](create-blob-object.md)

### Step 5: Create a tree object

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
    <a href="" style="float: left; margin-left: 10px;">Previous Step: .git folder</a>
    <a href="./2-blob-commit.html" style="float: right; margin-right: 10px;">Next Step: </a>
</footer>