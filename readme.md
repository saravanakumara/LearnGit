# Learning GIT

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
	
	**origin - is a alias name for your repo url. When we create a repo or clone a repo, Git will automatically creates this alias and we don't need to type the enitre URL every time while pushing the changes to the Remote repo. It is basically like a bookmark.**  
	
	**main - is a remote branch name that created by default when create a repo.**

**Check configured URL's**
`git remote -v` -> List the configured alias names for the remote repo URL's

## Branch
**Create branch locally**  

`git branch <branch name>` -> It will create branch locally.
	
**Modify branch locally**  

You should be in the branch and try change it by  

`git branch -m <branch name>` -> It will modify the branch locally that you are in.  

**Modify specific branch**  

`git branch -m <old branch name> <new branch name>` -> It will modify the branch locally that you are in.  

**Delete branch locally**  

You should be in the other branch for safe.  

*`git branch -d <branch name>`* -> It will Delete the branch locally.  

**Delete branch remotely**  

`git push origin --delete <branch name>` -> It will modify the branch locally that you are in.  

## Status
`git status` -> It will list down the changes done so far in the local repo.  

##