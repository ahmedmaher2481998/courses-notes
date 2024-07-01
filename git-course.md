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
