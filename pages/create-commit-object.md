---
layout: default
title: Create a tree object
---
### Step by step guide to create commit object

Here's an example of what a commit object might look like (simplified):
```
tree 2f3a123456789...
author John Doe <john@example.com> 1625592667 -0400
committer John Doe <john@example.com> 1625592667 -0400

Initial commit
```

***Step 1 - Prepare commit information:***

Since we are working with multiple lines, one way to achive this would be create a text file "commit.txt" for easier editing experience.
- Write the tree line with the SHA-1 hash of the tree object you created. (Since this is our first commit, we won't have a parent commit)
- Add author and committer information with your name, email and the current timestamp.
- Leave a blank line after the committer information and then write the commit message.

***Step 2 - Generate the Commit Object***
- Use the 'commit.txt' fi you made one to generate a SHA-1 hash for your commit object. This involves concatenating a header with the format `commit [size]/0` and the content of 'commit.txt'.
- Compress the content using zlib and store it in the `.git/objects` directory.

Here are the bash commands to achieve the above steps:

```
# Assuming tree SHA-1 is known and commit.txt is prepared
echo -en "commit $(wc -c < commit.txt)\0" > temp_commit
cat commit.txt >> temp_commit

# Generate SHA-1 hash
commit_hash=$(sha1sum temp_commit | awk '{print $1}')

# Compress and store
mkdir -p ".git/objects/${commit_hash:0:2}"
zlib-flate -compress < temp_commit > ".git/objects/${commit_hash:0:2}/${commit_hash:2}"
```

[Click here to return to creating first commit!](blob-commit.md)