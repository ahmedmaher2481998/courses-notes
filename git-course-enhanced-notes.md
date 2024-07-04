Reference: Pro Git (offline book available on Git website)

## History of Git

- BitKeeper is the reason Git exists.
- Git takes a snapshot of every delta that happens. Other version control systems used to take snapshots of the differences only. When you try to access a certain version, it replays all the incremental changes to reach the version you want.

## Git Architecture

- **Working tree, Git repository, and working directory**: The main folders you initialize Git in.
- We can only see one version in the working directory.
- **Requirements of making a new Git version control system**:
  - Track everything (objects, files, directories).
  - OS independent = portable.
  - Unique ID.
  - Track history and log of everything.
  - No content change.
- The things we keep track of can't be a unique ID, so we transfer it into an object.
- **Git objects**: There are four Git objects that Git keeps track of:
  - **Blob**: We track the content and the metadata (permissions, file size, and name, etc.).
  - **Tree**: Folder or directory content and metadata.
  - **Commit**.
  - **Tagged annotations**.
- To be OS independent, we transferred Git into a folder compressed, made easy encryptions. Also, it's portable.
- We made the Git repo folder inside the working directory named `.git`. This makes the working directory into a Git repo.
- A repo is a working directory containing `.git` repo.
- We hash the content of the files. When the hash changes, we know that the content of the files changed. The hash function is deterministic; it generates the same result with the same inputs every time (SHA-1 or 256/4 number of chars).
- Git uses SHA-1. Try: `$ git hash-object --stdin`.
- Also, Git adds additional data: type, size, and so on. This is how we generate the unique ID of the object.
- This is how Git knows you changed something.
- Git uses a 3-tree architecture: one is the working tree (WT), the other is the repo, and the last is the staging/index area (physically it's a file that is a middleman between WT and repo). We add to it by staging; we remove from it by committing.
- **The staging area has benefits**:
  1. We can change multiple files, but all changes are related, so we use the staging area as a stage before making only one commit.
  2. We can also use it as a stage to explore the difference between repo and WT.
  3. Untracked files are files not versioned by Git. We track it by `git add file`.
  4. When we track a file, we register it in the index area, we generate a SHA for it, and Git initializes a blob object for it. However, we only take the snapshot when committing it.
  5. **File states**:
     - Untracked (U).
     - Tracked - modified (M: we made changes in the WT but not committed to the repo).
     - Unmodified (repo and WT have the same version of this file, has no symbol).

## Basic Git Commands

1. **Configure name and email**:
   ```bash
   $ git config --global user.name "name"
   $ git config --global user.email "email"
   ```
   --global means by user. If you want it to be really global, use --system.
2. **Initialize a Git repo**:
   `bash $ git init `
   This adds a .git folder to the WT (working directory)
3. **List all staging files**:
   `bash  $ git ls-files`
   To see all files in the repo:
   `bash $ find .git/objects/ -type f`
4. **Add file to staging**:
   `bash $ git add filename | src/ .ts | . | filenamestart*`
   Files added to the index are marked as (A).
5. **Add .gitignore and commit**:
   `bash $ git commit -m "commit message"`
   To remove from staging:
   `bash $ git rm --cached filename`
6. **View file type, size, and content**:
   ```bash
   $ git cat-file -t <index sha>
   $ git cat-file -s <index sha>
   $ git cat-file -p <index sha>
   ```
   Add a message to notify what this version represents:
   `bash $ git commit -m 'msg'
`
