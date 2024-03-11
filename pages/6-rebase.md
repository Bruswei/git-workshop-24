---
layout: default
title: Merge And Rebase 
---

Most of us have probly used `git rebase `on another branch before. Just in case here is a quick sum up what rebase is doing:

> Git rebase rewrites the commit history by transferring commits from one branch to another, creating a linear sequence. It's used for cleaner project history but requires caution on shared branches to avoid issues. This is another way of explaining:
> ```
> main:       1 --- 2 --- 3
>                   \
> feature:           A --- B --- C
> ```
> After rebasing feature (that contains commit A, B and C) on main:
> ```
> main:       1 --- 2 --- 3 --- A --- B --- C
> ```

Let's delve into the internal mechanics of rebasing in Git. Initially, a Git branch is essentially a pointer to a specific commit, which in turn is linked to its ancestor commits, forming a chain that traces back to the initial commit in the repository. However, the scenario becomes more complex when we decide to rebase a feature branch onto an updated main branch.


## Make a new branch and a commit

1. Let's make a new branch that is pointing to main and update HEAD, make it as an exercise do it manually instead of `git checkout -b `. For workshop purpose, name it "gitignore".

2. Now lets make a new file `.gitignore` with command `touch .gitignore` and leave it empty. 

3. Make a new commit and make sure it is on the new `gitignore` branch! If you want you can do it manually as we did earlier. If not just commmit to the new branch you just made.

Verify that you have commited two branches from main with `git log --oneline --graph`.


## Fast-forward merging

Now lets merge our `main` branch so the new branch `gitignore` is behind and ready for rebasing.

This is how it looks now:

```
    Main
   /    \
Dev      Gitignore
```
With a fast-forwarding merging the new graph should looks like:

```
  initial commit
   /        \
Dev/Main     Gitignore
```

Lets give a try and see if you can achive this outcome without assistance from what we have learned from earlier, if not you can click below to show the steps. 
<details>
  <summary>Click here to expand!</summary>
    <br>
  Since what we are trying to achive here is just pointing main to the same commit object as dev, we can just easly copy the hash-id of `.git/refs/heads/dev` and paste it into `.git/refs/heads/main`.
</details>
  <br>

## Lets do some Rebasing

Now lets checkout how the git graph looks like, we can do it with command `git log --oneline --graph gitignore main`, this is how it looks like on my screen:

```
* 791517b (HEAD -> gitignore) Add gitignore
| * 782a959 (main, dev) Update readme
|/  
* 79e1fd1 Initial commit
```

Now we can see there are two different path from initial commit which indicates `gitignore` and `main` have diverged. This is where rebase comes in. Normally we can run `git rebase main` when checked out `gitignore` branch, but lets do this manually.



