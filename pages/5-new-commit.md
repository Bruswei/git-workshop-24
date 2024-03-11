---
layout: default
title: Understanding Git's Behavior
---

Let's update the README.md file to include an additional exclamation mark, and then explore how Git processes this change.

```
This repository was made manually without git init!!
```

Lets make the commit in the usual way and lets observe what git does here. Use `git add README.MD` and `git commit -m "Update readme"` and then run command `tree .git` to check the structure. Can you identify the new objects and see what has changed here?

<!-- Use command `git cat-file -t insertYourObjectIdHere` to check the type of the objects.  -->

### Understanding Git's handling of changes:

1. Execute git log in your terminal to view the most recent commits. You'll notice a new commit titled "Update readme". Copy this commit's hash, then use git cat-file -p <yourHashId> to inspect the commit object. You'll see it contains fresh data and a link to its parent commit, which is the initial commit you created.
2. Locate and copy the hash (of tree object) found within this commit object and inspect it using git cat-file -p <yourHashId>. This operation should reveal that README.md is associated with a new hash, different from the previous one.
3. Extract and inspect the hash from the tree object linked to this commit by running git cat-file -p <yourHashId>. You will find that it displays the content: This repository was made manually without git init!!, indicating the update made to README.md.

### Summary of Git's behavior:
By adding a single "!" to README.md, git creates three new objects: a blob, a commit, and a tree object. This demonstrates Git's efficient change tracking, where each content modification generates a unique hash, serving as a checksum to quickly identify changes. Something else very interesting, Git retains old objects, enabling swift version transitions without recalculations, as all blobs and trees are compressed and stored. 

Consider a scenario where another file remains unchanged while you modify only one file in the repository. How do you think the structure of your .git directory will adapt to this change? Will Git create new blobs and trees even if only a single file has been updated? 

<footer style="width: 100%; display: flex; justify-content: space-between; padding: 20px 0;">
    <a href="./4-branch.html" style="float: right; margin-right: 10px;">Back to: Branching</a>
    <a href="./6-rebase.html" style="float: left; margin-left: 10px;">Next: Rebasing</a>
</footer>