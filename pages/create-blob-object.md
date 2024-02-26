---
layout: default
title: Create a blob object
---

### Step 1: Prepare the content with the header
Prepare the Content with the Header: Create a temporary file that starts with the header (blob <size>\0), where <size> is the size of your README.md file in bytes, followed by the content of the README.md file. The \0 represents a null character. This is not too important for us to understand Git internals.

```
file_size=$(stat -f"%z" README.md)  # Use `stat -c"%s" README.md` on Linux
echo -n "blob $file_size\0" > temp_object
cat README.md >> temp_object
```

### Step 2: Compress Using zlib:
Git uses compression to efficiently store its internal objects, this is crucial for minimizing disk space usage and performance. However it is not crucial for the goal of this workshop. 

To compress, run following command with python:

```
python3 -c "import zlib,sys; sys.stdout.buffer.write(zlib.compress(open('temp_object', 'rb').read()))" > compressed_object
```

### Step 3: Store the Object Manually
Create the Correct Directory Structure: The first two characters of the SHA-1 hash you obtained in Step 1 form the directory name within .git/objects, and the rest of the hash is the filename.
```
# Assuming the hash is stored in a variable `hash`
hash=$(git hash-object README.md)
objects_dir=".git/objects/${hash:0:2}"
mkdir -p $objects_dir
object_file="${objects_dir}/${hash:2}"
```

Move the Compressed Object: Move or rename the compressed_object to the path you just created.

```
mv compressed_object $object_file
```

Congratulations, you have now created your first blob object manually.

### Step 4: Lets verify

After completing these steps, let's take a look at what's happened inside our `.git` folder. You'll find a new directory in `.git/objects`, with `35` as the leading folder name and the remainder of the hash following it.

``` 
.git/objects
├── 35
│   └── d7a9a460c597c8a29b210b2bed894a5281088e
├── info
└── pack
```

Now lets see what happens when we run `git cat-file 35d7a9`. It should show exactly the content that you have added in README.md. If you followed the instructions exactly then it should show:
Now, when we execute `git cat-file -p 35d7a9` or `git show 35d7a9`, it should display the content you've added to `README.md`. Assuming you have followed the instruction precisly, you should see: 
```
This repository was made manually without git init!
```

As we expected, a blob object only contains the data of the files. In our case, we only have a the content of `README.md` saved, no meta datas are saved such as the name of the file.

**Note: Did you find it curious that the hash from your `README.md` file matches the one mentioned here before you even hashed it on your machine? That's Git's magic at work, utilizing SHA-1 hashing to create a checksum for the objects. If the hash in your `.git` folder matches the one here, it indicates that the files are indentical according to Git.**

[Click here to return to creating first commit!](blob-commit.md)