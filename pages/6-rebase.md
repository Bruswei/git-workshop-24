---
layout: default
title: Merge And Rebase 
---

Many of us are familiar with using git rebase with branches, but here's a brief recap of what rebase does:

>Git rebase modifies the commit history to move commits from one branch to another, creating a straight-line sequence. This method is favored for achieving a cleaner project history but demands careful handling when dealing with branches shared with others. To illustrate:
> ```
> main:       1 --- 2 --- 3
>                   \
> feature:           A --- B --- C
> ```
> After rebasing feature (that contains commit A, B and C) on main:
> ```
> main:       1 --- 2 --- 3 --- A --- B --- C
> ```

Let's explore how rebasing works behind the scenes in Git. A branch in Git points to a specific commit, which links back to its predecessor commits, creating a historical chain back to the initial commit. Rebasing a feature branch onto an updated main branch complicates this straightforward lineage.

## Creating a new branch and commit

1. Create a new branch called "gitignore" that points to the main branch. Do this manually for practice, instead of using git checkout -b. 

2. Use touch .gitignore to create a new .gitignore file, leaving it empty.

3. Commit this new file to the gitignore branch, either manually or with the usual commit commands.

Verify that you have commited two branches from main with `git log --oneline --graph`.

## Fast-forward merging

We'll now merge the main branch so that the gitignore branch falls behind, setting the stage for rebasing.

Currently, the branch layout is:

```
    Main
   /    \
Dev      Gitignore
```
After a fast-forwarding merging the new graph should looks like:

```
  initial commit
   /        \
Dev/Main     Gitignore
```

Try to achieve this based on what we've learned. If you need a reminder, you can expand the instructions below.
<details>
  <summary>Click here to expand!</summary>
    <br>
    To align `main` with `dev`, simply copy the commit hash from `.git/refs/heads/dev` and paste it into `.git/refs/heads/main`.
</details>
  <br>

## Lets Rebase

Now lets checkout how the git graph looks like, we can do it with command `git log --oneline --graph gitignore main`, this is how it looks like on my screen:

Review the git graph for the `gitignore` and `main` branches with `git log --oneline --graph gitignore main`. It might look like this: 

```
* 791517b (HEAD -> gitignore) Add gitignore
| * 782a959 (main, dev) Update readme
|/  
* 79e1fd1 Initial commit
```

This indicates gitignore and main have diverged. Here's where we typically use git rebase main from the gitignore branch. However, let's break down what happens internally during a rebase:

> 1. Identifies base common commit: Git finds the common base commit between the two branches, which is `79e1fd1` from the graph above (or your initial commit).
> 2. Replay changes: Git takes commit from the `gitignore` branch that are not in `main`(in this case `79e1fd1`) and replays them on top of `main`. Since `main`'s latest commit is `782a959`, Git attempts to apply the changes from `791517b` onto this commit. 
> 3. Create new commit objects: Each commit applies to the new base creates a new commit object because the parent commit changes(from `79e1fd1` to `782a959`), even if the file content (blobs) doesn't change. This new commit object will have a new SHA-1 hash because its metadata (such as parent commit) changes.
> 4. Update branch reference: Finnaly, the `gitignore` branch reference is updated to point to the newly created commit, effectively moving the branch on top of the `main`.

To achive this we can use porcelain command `cherry-pick` which applies the changes from specific commits to the current branch as new commits. 

1. Change your HEAD to reference main (or just a `git checkout main`)
2. Make a temp branch either by copy in `.git/refs/heads/main` or just `git checkout -b temp`
2. Run `git cherry-pick <your-gitignore-branch-id>`
3. Update gitignore branch refernce to the same as temp branch.


Now you can verify the correct sturecture in your git graph with `git log --oneline --graph`.


<footer style="width: 100%; display: flex; justify-content: space-between; padding: 20px 0;">
    <a href="../index.html" style="float: left; margin-left: 10px;">Return to first page</a>
</footer>