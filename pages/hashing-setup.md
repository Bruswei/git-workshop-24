---
layout: default
title: SHA-1 Hashing Across Different Operating Systems
---


SHA-1 is a cryptographic hash function used by Git to uniquely identify objects within the repository. Here are the methods to perform SHA-1 hashing manually on different operating systems:

### Windows

On Windows, the built-in `CertUtil` tool can be used to generate SHA-1 hashes. To do this, open Command Prompt and enter the command `CertUtil -hashfile pathToFile SHA1`, replacing `pathToFile` with the actual path to the file you wish to hash.

### Mac

For Mac users, the `shasum` utility is available by default and can be used to compute SHA-1 hashes. Open the Terminal and type `shasum -a 1 pathToFile`, making sure to substitute `pathToFile` with the correct file path.

### Linux

Linux users can utilize the `sha1sum` command to perform SHA-1 hashing. In the Terminal, enter `sha1sum pathToFile`, again replacing `pathToFile` with the path to the file that needs to be hashed.

Remember to replace `pathToFile` with the actual file path for which you want to compute the SHA-1 hash on all operating systems.
