reference is pro git offline book is available on git website

- history of git ,git BitKeepers is the reason git to exist,Git take snap shot from every delta that happens other version control systems used to take snap shot of the differences only and whe you try to access a certain version it replays all the incremental changes to reach the version you want .
- git architecture
  - working tree , git repo ,working directory is the main folder you initialized git in it
  - we can only see one version in the working directory
  - requirement of making a new git version control system
    - track everything {objects , files , directories} , os independent = potrable,unique id ,track history and log of everything,no content change
    - the things we keep tracking of can't be unique id so we transfer it into an object
    - git objects there four git objects that git keeps tracking of ( blob:we track the content and the meta data(permissions ,file size and name and so on ) , tree: folder or directory content and metadata ,commit , tagged annotations )
    - to be os independent we transferred git into a folder compressed made easy encryptions also it's portable
    -we made the git repo folder inside the working directory name as .git this makes the working directory into git repo 
   - a repo is a working directory containg .git repo
   - we hash the content of the files when the hash changes we know that the content of the files changed  the hash function is deteminastice it generates the same result with the same inputs every time  hsa-1 or 256 /4 no of chars 
   - git uses sha 1 try  $ git has-object --stdin 
   - also git adds aditional data type,size and so on and this is how we generate the unique id of the object 
   - this is how git knows you changes something 
   - 2 tree archtecture but git uses 3  tree arch one is wt the other is repo and last is staging/index area physically it's a file that is a middle man between wt and repo we add to it by staging we remoive from it by commiting  
   - the staging area has benifits 
   	1 . we can change multiple files but all changes are related so we use the staging area as a stage before making only one commit 
	2 . we can also use it a stage to explore the difference between repo and wt
	3 . un-tracker files is files not verisioned by git we track it by by git add file 
	4 . when we track file we regiter it in the index area we generate a sha for it and git init a blob object for it but we will onlu take the snap shot when commiting it  
	5 . file states : untracked U, tracked - modified M (we made changes in the wt but not comitted it to the repo),unmodified repo and wt has the same version of this file has no symbole  
- we start by configure name and email 
git config --global user.name "name" , user.email "email" gloable mean by user if you want it to be realy global we use --system 
- we init a git repo using git init this adds .git folder to the wt (working directory)
-  git ls-files listall staging files,to see all files in repo find .git/objects/ -type f to find all files in repo 
- 1 git add filename | src/  .ts | . | filenamestart* (staging) A added to index 
- 2  add .gitignore , git commit -m "comiit message" , to remove from staging git rm --cahced filename 
- 3 git cat-file -t (index sha) return the type of the file  if we added option -s we get the size and -p for content,git commit -m 'msg' we add a message to notify us what this version represents timeline description
- 4 git status,the repo has objects for blob treemhow to know that the tree object and blob objects related the the same patch ,git solved this by creating commit object that descripe the content of each patch and by whom and when and who to reach the current version,commit is a snapshot|bookmakr|patch or other names ,the commit points to that tree that points the files of this patch we stopped at v7 start:00.00
- 5 git status -s relveals the status in short form ,M red means modified but in synced in index/staging area or in repo ,M grren means modified but synced only in staging area,there's a parent detail added to  each commit it points to the parent commit the parent is not added to the first commit 
- 6 dsa used is linked list ,the first branch is defaulted to master by git,head is the current version we are showing, we can move head back and forward 
- 7 to know the diff between commitis $git diff shows the diff between the three trees ,if we git add . and then git diff we see nothing if we needed the diff between repo and staged we use git diff --staged  ,wehn commiting we can git commit with no message and git will open the defalut editor which can be configure by git config --global core.edit "code | nvim | vim" we then add title and desc if needed 
- 8 git log --oneline ,git log filename.extension ,git log -2 last two commites ,--graph ,git show commit , tels you the commit changes that hapend in that commit
- 9 the diff between commites,git diff firstcommit .. lastcommit to rename/move file use git mv 
- 10 to untrack file $git rm --cached filename,to discard $git restore filename ,git restore --staged to unstage file,git commit -am msg addes and commit in the same command ,to modifiy the last commit message git commit --amend ,we can traverse the wt by changing commits ,when trying to go back in revision we apply it to staging best practice ,git reset Head /~1 one commit backword  /add --hard to apply on working tree ,Head is a pointer to the current wt commit ,git reflog logs of the HEAD moves ,git reset --hard @{4} this anotation is result of git reflog ,to un commit or revert commit we use git revert commitref
11 - tags :
	1- we tag commit for versioning we have light weight tag an anotited tags 
	2- git tag -a version -m msg ,git show v2.0/tag version to make things easier 
	3- and this is the last object type 
12 - branching ,for better logs :git log --oneline --decorate --graph ,create new branch git branch branchname ,
git branch to view all brances ,git switch branchname ,now if we added commites it won't be added to the master branch but added to branchname branch and the head movies towards the new commit on the ne wbrnach to observe better git log --graph --oneline --decorate we change branches using git switch now if we are okay with changes we need to merge ,git switch master ,git merge brancname,to merge we first go to the source branch and then we can delete it ,git branch --merged shows the branced merged into master ,to delete branch git branch -d branchname ,usually we add then diverte from master again 
13 -head is the defining factor of the working tree shape , if master has some changes after se diverded from it when last merged or taked new branch , merge here is called three way merge in order for git to place things together better it creates new commit and place it as head for the branch we trying to merge into and by this it can merge new from the master to old from branchname toghether in a single branch that is now master,how to resolve confilects ,
14 - git rebase is some kind of merge but it squash things together 
15 - remote repo upstream to push to,downstream/fetch pull we can connect to more than a remote repo ,git remote ,hosting service github
16 - git -u push origin ,git fetch && git merge === git pull ,remote repo and local repo are not always aware of each others changes ,so you need to push and pull to keep things up to-date,git remote outputs the name of the remote repo origin ,git remote -v ,out puts remote location ,to get the remote branches git brance -r , we first fetch changes them then merge them ,to know your current state with remote fetch first then git status , when you create new branch you need to push it and set it as upstream $git push -u origin  ,git branch -vv each branch and it's tracking origin,make more search regarding git stach  
17 - vs code extensions,git lens , git graph (github desktop,git kraken) hit hub is a hosting service for git 
