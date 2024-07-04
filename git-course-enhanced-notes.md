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
7. **Check status**:
   `bash Check status`
   The repo has objects for blob and tree. To know that the tree object and blob objects relate to the same patch, Git solved this by creating a commit object that describes the content of each patch, by whom, when, and who to reach the current version. A commit is a snapshot, bookmark, patch, or other names. The commit points to that tree that points to the files of this patch.
8. Short status:

`bash $ git status -s`
. M (red) means modified but not synced in the index/staging area or repo.
. M (green) means modified but synced only in the staging area.
. There's a parent detail added to each commit; it points to the parent commit. The parent is not added to the first commit.

9. **Data structure used**:

- Linked list.
- The first branch is defaulted to master by Git.
- HEAD is the current version we are showing; we can move HEAD back and forward.

10. **To know the diff between commits**:

    ```bash
    $ git diff
    ```

    Shows the diff between the three trees. If we:

    ```bash
    $ git add .
    ```

    And then:

    ```bash
    $ git diff
    ```

    We see nothing. If we need the diff between repo and staged:

    ```bash
    $ git diff --staged
    ```

11. **Committing**:

    ```bash
    $ git commit
    ```

    Without a message, and Git will open the default editor which can be configured by:

    ```bash
    $ git config --global core.editor "code | nvim | vim"
    ```

    We then add a title and description if needed.

12. **View commit logs**:

    ```bash
    $ git log --oneline
    $ git log filename.extension
    $ git log -2
    $ git log --graph --online --all --decorate
    $ git show <commit>
    ```

    Tells you the commit changes that happened in that commit.

13. **Diff between commits**:

    ```bash
    $ git diff <first commit>..<last commit>
    ```

    To rename/move a file:

    ```bash
    $ git mv <old filename> <new filename>
    ```

14. **To untrack a file**:

    ```bash
    $ git rm --cached filename
    ```

    To discard changes:

    ```bash
    $ git restore filename
    $ git restore --staged filename
    ```

    To add and commit in the same command:

    ```bash
    $ git commit -am "msg"
    ```

    To modify the last commit message:

    ```bash
    $ git commit --amend
    ```

15. **Traversing the WT by changing commits**:
    ```bash
    $ git reset HEAD~1
    ```
    To apply on the working tree:
    ```bash
    $ git reset --hard HEAD~1
    ```
    HEAD is a pointer to the current WT commit. Git reflog logs the HEAD moves:
    ```bash
    $ git reflog
    ```
    To uncommit or revert a commit:
    ```bash
    $ git revert <commit ref>
    ```

## Tags

1. We tag commits for versioning. We have lightweight tags and annotated tags.
2. Create a tag:
   ```bash
   $ git tag -a <version> -m "msg"
   ```
   Show tag:
   ```bash
   $ git show <tag version>
   ```

## Branching

1. For better logs:
   ```bash
   $ git log --oneline --decorate --graph
   ```
2. Create a new branch:
   ```bash
   $ git branch <branchname>
   ```
3. View all branches:
   ```bash
   $ git branch
   ```
4. Switch to a branch:
   ```bash
   $ git switch <branchname>
   ```
   Now if we added commits, it won't be added to the master branch but added to the `<branchname>` branch, and the head moves towards the new commit on the new branch. To observe better:
   ```bash
   $ git log --graph --oneline --decorate
   ```
   We change branches using `git switch`. Now if we are okay with changes, we need to merge:
   ```bash
   $ git switch master
   $ git merge <branchname>
   ```
   To merge, we first go to the source branch and then we can delete it:
   ```bash
   $ git branch --merged
   $ git branch -d <branchname>
   ```
   Usually, we add then diverge from master again.

## HEAD

- HEAD is the defining factor of the working tree shape. If master has some changes after diverging from it when last merged or taken a new branch, the merge here is called a three-way merge. In order for Git to place things together better, it creates a new commit and places it as HEAD for the branch we are trying to merge into. By this, it can merge new from the master to old from `<branchname>` together in a single branch that is now master. This is how to resolve conflicts.

## Rebase

- `git rebase` is some kind of merge but it squashes things together.

## Remote Repository

1. **Upstream**: To push to.
2. **Downstream/fetch/pull**: We can connect to more than a remote repo.
3. View remote:
   ```bash
   $ git remote
   ```
4. Hosting service: GitHub.
5. Push origin:
   ```bash
   $ git push -u origin
   ```
   Fetch and merge:
   ```bash
   $ git fetch && git merge
   ```
   This is equivalent to:
   ```bash
   $ git pull
   ```
   Remote repo and local repo are not always aware of each other's changes, so you need to push and pull to keep things up-to-date.
6. View remote branches:
   ```bash
   $ git branch -r
   ```
   Fetch changes, then merge them:
   ```bash
   $ git fetch
   $ git status
   ```
   When you create a new branch, you need to push it and set it as upstream:
   ```bash
   $ git push -u origin
   ```
   View each branch and its tracking origin:
   ```bash
   $ git branch -vv
   ```
   Search for more information about Git stash.

## VS Code Extensions

- GitLens, Git Graph (GitHub Desktop, GitKraken).
- GitHub is a hosting service for Git.

## Basic Git Workflow

1. Clone the repo. The proper workflow is to create the repo locally, then push it upstream:
   ```bash
   $ git branch -M <new branch name>
   $ git branch -m <rename branch>
   ```

## GitHub Interface (continued)

- Cloning means to get all the repo's history besides the code itself.
- The main way to initialize a new repo is to create a new local repo and then connect it to an empty remote repo.
- Get all branches:
  ```bash
  $ git branch --all
  ```
- You can't push upstream unless you are authenticated with GitHub.
- The best way to authenticate your CLI is via SSH.
- Always try to clone and add remote using SSH. GitHub uses SSH to verify your identity each time you try to use it.
- You can locally generate SSH keys and then add them to your GitHub account settings.

## Managing Remotes

- Search on how to remove remote and managing multiple remotes.
- More info about Git & GitHub workflow.

## Contributing to Open Source: A Guide Using Git and GitHub

1. Fork the repo, then clone the forked repo.
2. Always keep the forked repo updated by fetching updates from GitHub.
3. Add a new remote for the real repo that you forked. Now, you have two remotes so you can fetch updates from the real remote and then push to your own forked version of it.
4. Always use the name when pushing:
   ```bash
   $ git push <remote> <local branch>
   ```
5. Apply for a pull request for the real remote to apply your changes. The maintainer can either close/ignore the pull request or accept/remove it.
