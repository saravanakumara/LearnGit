# Learning GIT

## Key Pointers
1. **HEAD**  
	Current location - *'You are here'* sticker
2. **main**  
	Local primary branch
3. **origin\main**  
	Local bookmark for remote server - to track

## Repo setup
*Creating a repo via general GIT command line is not possible. Remote server i.e GitHub is allowed to create via GitHub command line tool.*  

With normal GIT command line tool:
1. First, create a repo on the GitHub site.
2. Note down the repo URL.
3. In local system, create a folder name with the repo name that is provided during the repo creation on the Step1.
4. Once created repo folder, run the below command to initialize the empty git repo  

	`git init`  
	
	*"main" branch will be created on the remote repo by default."*  
5. Create any files you would like to add to the repo i.e the files are ready to stage and commit  

	`git add <path to the file name> <path to the file name>`
6. Once the files are ready, the changes will be committed to the local repo by  

	`git commit -m <commit info>`
7. Now these changes are ready to push to remote server (repo)
8. Create a link to the remote Repo from your local repo by,  

	`git remote add origin "https://github.com/<project/user name>/<repo name.git>"`  
	
	*"git remote" is used to edit a configuration file on your own computer i.e it will update the .git/.config file on the local system*
9. Once alias/link is created with remote repo, we can push the changes to the remote repo by,  

	`git push origin main:main` i.e pushing the changes to the remote server repo that is 'origin' or 'https://github.com/<project/user name>/<repo name.git>' from local 'main' branch 'any' remote branch. This can be simplified as both branch name are main,  
	
	`git push origin main`. If branch name is different, `git push origin <local branch name>:<remote branch name> for example, git push origin apple:banana`
	
	#### Note
	1. **origin** *is a alias name for your repo url. When we create a repo or clone a repo, Git will automatically creates this alias and we don't need to type the enitre URL every time while pushing the changes to the Remote repo. It is basically like a bookmark.*  
	
	2. **main** *is a remote branch name that created by default when create a repo.*

### Check configured URL's
`git remote -v` -> List the configured alias names for the remote repo URL's

## Branch
**Create branch locally**  

`git branch <branch name>` -> It will create branch locally.

**Switch branch**  

`git checkout <branch name>` -> It will switch to the branch mentioned.
	
**Modify branch locally**  

You should be in the branch and try change it by  

`git branch -m <branch name>` -> It will modify the branch locally that you are in.  

**Modify specific branch**  

`git branch -m <old branch name> <new branch name>` -> It will modify the branch locally that you are in.  

**Delete branch locally**  

You should be in the other branch for safe.  

*`git branch -d <branch name>`* -> It will Delete the branch locally.  

**Push new branch**  

1. If branch is already available on the remote repo, they changes will be uploaded. [You should create a branch in the remote repo server before] 

`git push origin <branch name>`  

	1. We can simplify the command by setting up upstream for this branch at first push and this upstream is alive until branch deleted.
		`git push --set-upstream origin <branch name>'
	2. Next time onwards the push command will be,
		`git push` [no need to mention remote name and branch name]  

2. If branch is not available on the remote repo, we will get fatal error **No upstream for the branch.** [You should create a branch in the remote repo server before]

**Delete branch remotely**  

`git push origin --delete <branch name>` -> It will modify the branch locally that you are in.  

## Status
`git status` -> It will list down the changes done so far in the local repo.  

## Merge
*Merge the changes of one branch to other branch i.e basically merge fetaure branch to main branch*  

*Merge will preserve the git history and it is mainly used in projects*
`git checkout master`
`git merge <feature/bugfix branch name>`
	#### Before merge
	In the master branch A->B
		1. Create new branch and checkout
		2. HEAD is pointed to local feature branch B pointer
		3. main is pointed to local feature branch B pointer as main 
		4. origin\main is pointed to remote main/master branch i.e pointer B
	#### After merge
	In the master branch A->B
		1. HEAD is pointed to main branch of master branch where we checked out
		2. A->B->D->C->M(Which is merge commit pointer. It links the both branches and will have 2 parent pointers)
		3. Now HEAD is pointed to Merge pointer
		4. main is pointed to Merge pointer
		5. origin\main is pointed to remote main/master branch i.e pointer B
		6. `git push origin master` -> to update on the remote server

## Rebase
*Rebase, update the changes of one branch to other branch i.e basically change the base of fetaure branch to main branch base*  

*Rebase will rewrite the git history to maintain cleanliness and it is mainly used in private repo*
`git checkout feature`
`git rebase main`
	#### Before rebase
	In the master branch A->B
		1. Create new branch and checkout
		2. HEAD is pointed to local feature branch B pointer
		3. main is pointed to local feature branch B pointer as main 
		4. origin\main is pointed to remote main/master branch i.e pointer B
	#### After rebase
	In the master branch A->B
		1. HEAD is pointed to local branch
		2. main is pointed to local branch
		3. origin\main is pointed to remote main/master branch i.e pointer B
		4. A->B->D->C'(Which is a new commit where the new changes from local branch is recommitted again. It will remove the old commits on the local branch).
		5. Now main is pointed to D pointer
		6. main is pointed to D pointer
		7. `git push origin <branch name> --force-with-lease` -> Force push to update on the branch PR, otherwise normal push will not work as previous PR will have different history and now it will have different history. So force push is needed here.

## Conflict resolve
1. When user A made some changes on the class A file and committed, pushed for merge to master.
2. When user B made hotfix channges on the class A file and committed, pushed for merge to master, hotfix branches.
3. Now conflicts occurred,  
	1. We need to open the conflict file and look for conflict pointers like `<<<< HEAD file contents ====== file contents >>>> branch name`.
	2. Review and keep the required changes by manually removing the unwanted conents that conflicts created and save it.
	3. Now `git add <conflict resolved file name>.`
	4. Commit `git commit -m "conflict resolved info message".`
	5. Push the changes `git push origin <branch name>.` or `git push origin <branch name> --force-with-lease`
	6. Also we can use `git rebase --abort` or `git rebase --continue (after Conflict)`
