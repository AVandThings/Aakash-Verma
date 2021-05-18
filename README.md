
GIT README:
-----------

Repo is the collection of files managed by git. 
.git folder contains the git repo. 

Local Git States: 
1. Working Directory 
2. Staging area	
3. Repository 

4. Remote state --> Remote repo 


.git folder tracks your repo. So, deleting it will remove the git tracking for the folder 


git add < filename > 		-> move file to staging area. 
git add .			-> To add all the files in the repo 

git status 			-> check git status 

git commit -m "<message>" 	-> commit the changes in staging area.   
git commit 			-> Open the default editor for commit message 
git commit -a 			-> Add and commit, so you can skip the "git add" command

git log 			-> log of all the commits 

git show 			-> to view all the commit's diff
git show <sha> 			-> to view a particular commit's diff 

git ls-files 			-> Files being tracked by git 

Unstage the change: 
-------------------
git reset HEAD <filename>	-> Unstage the changes 
git checkout -- <filename>	-> To revert back to the last working changes


git help log 			-> to get help page of "git log" command


git config --global alias.<new cmd name > "<your cmd>"		-> To create alias of a git command, 
							 	   Use - git <new cmd name>

Rename file name on git: 
------------------------
git mv <filename> <new filename>	-> This will only stage the file, then commit the file to the git. 
					   
If you simply use the mv command to rename, git will track this as 
deletion of old file and show the renamed file as untracked. 

To update the git repo, in the above case, 
git add -A     				-> This will consider all the modifications done on the file, 
					   including name change, as file update. After this simply 
					   commit the change. 
					

git rm <filename>			-> To remove the file from the git. But this is only staged, so 
					   you have to commit it on the git. if you use rm command to remove
					   the file, then follow the steps as mentioned above for mv. 

Exclude files from a repo:
--------------------------
touch .gitignore			-> create the .gitignore file
					-> for exmaple: log files

in .gitignore file mention the file to be ignored or you can use a wildcard "*".
then commit this in the repo. 


git diff <commit 1> HEAD		-> To get the diff b/w the head and commit
git diff .				-> get the difference b/w HEAD and working dirs.

git diff <branch 1> <branch 2>		-> To get diff b/w branches

git difftool <commit 1> HEAD		-> Uses "git diff" but with a tool such as p4merge


HEAD 					-> Points to the last commit of the current branch. 


Branching and Merging:   
----------------------
git branch 				-> Show the branches 

git checkout -b <branch name to create> -> the -b option creates a new branch and the checkout switches
					   to that branch. 

git checkout <branch name>		-> switch to the branch. Branch name can be a remote.  

git merge <branch name>			-> This merges the branch specified into the current branch 
					   which we are in. 

git branch -d <name>			-> The -d option deletes the branch specified 


In case of merge conflict, in simple case modify the file. You can also use a merging tool. 

In the conflict state, 
git mergetool 				-> This will launch the merge tool, eg. p4merge. 

Then commit the changes. 
There will be ".org" file created that will be the original file. 

git push -u <remote name> <new local branch name>	-> This will push the new branch and -u option
							   will setup the tracking relationship 


Git Tags: 
---------
git tag <tag name>			-> Creates a lightweight tag 

git tag -d <tag name>			-> This will delete the tag. 

git tag -a v1.0 -m "<Commit message>"	-> To add tag name (-a option) and commit message (-m option)

git show <tag name> 			-> This shows the tag and commit details. 


Stashing:  	
---------
git stash 				-> Saves the last work-in-progress files and you will have a 
					   clean working directory.  

git stash list 				-> list all the stashes and the last commit and the associated
					   commit message 

git stash pop 				-> Puts the changes saved earlier and drops the stash that was
					   applied. 


Time Travel:  
------------
git reset <commit id> --soft 		-> It change where head is pointing to the commit mentioned.
					   It preserves the staging area and our working directory. 

git reset <commit id> --mixed 		-> default option. 

git reset <commit id> --hard 		-> Hard reset and change the Head and doesn't preserves the 
					   staging area. 

git reflog 				-> Shows all the different actions taken in the pwd. 
					   Now you can switch to a particular commit. 


Linking to git repo:  
--------------------
git remote -v 					-> Shows all the remote connections

git remote add <remote name> <url of git repo>	-> This will add a connection b/w local and git repo
	

Pushing to the git repo: 
------------------------
git push -u <remote repo name> <local branch name> --tags  
						-> -u option sets up a tracking branch relationship
						   b/w the local branch and the git repo. The --tags 
						   pushes all the tags in the current local repo.
						   local branch can be a new branch created locally. 

git push <remote> <local branch>		-> Push the files to github server.

git push 					-> Push the code to current tracking branch to the 
						   remote git repo.   

git push <remote> :<branch name>		-> This will tell the git to delete the branch after ":".

git config --global push.default simple 	-> Need for git push for GIT v2.0 and after.


Setting up ssh auth: 
--------------------
Create a .ssh directory in your working directory. Mine is at ~. 
Then move to .ssh dir. 
Then generate the ssh key of type rsa using, 
		shh-keygen -t rsa -C "<email address>"
Then press enter. 
You may or may not use a passphrase. 
After this your public and private keys is generated and will be saved as "~/.ssh/id_rsa" 
and ".ssh/id_rsa.pub" file. The pub file is you public key and other is private key.  

Copy the id_rsa.pub file's contents and in git hub and paste it on github add ssh key. 

use below command to verify, 
			ssh -T git@github.com
You will be prompted for successful login. 


Git Repository: 
---------------
git clone <SSH Clone URL>		-> This will clone the remote git repo. and by default it sets
					   the origin to the cloned repo. on github. 

git clone <URL> <name of folder on local>	-> This clones the repo in the folder, with the name
						   provided in the clone command. 

  
git pull 				-> This is 2 commands, "git fetch" and "git merge". So, it will
					   first fetch then merge the code. 

git pull --all 				-> Update all tracking branches. 

git fetch 				-> Update the local repo details from github


git remote set-url <name of remote ref>	 <new git URL>	-> Updating reference to origin, do this
							   if the remote repo name is changed. 

git remote show 			-> To get the remote origin details 


Pull Requests: 
--------------
-> Pull request are used to merge 2 branches. It will compare the 2 branches and will generate pull 
   request. Only the repo owner can merge this to mainline. This is done from the github website. 

For local changes, 
switch to master branch. -> do git pull to get latest code. 
git merge <name of branch to merge to master>	-> This will merge the branch name provided to master.
git push 					-> To sync the changes. 

then, delete the branch, 
			git branch -d <name of the branch>

Now, remove the references of the deleted branch, 
			git fetch -p 	

Now, "git branch -a" will show the new branch list. 


git fetch 				-> To update the references 


Rebase:  
-------
It rewind the commits of branch you are merging in to the point where the branch originally diverged 
and play back commits that happened on the branch you are trying to merge and then playing the commits
that were on the branch that you are currently on. Now the changes that happened on remote will be after
the once on your local branch. 

git pull --rebase 


git log --online --graph 		-> Shows the branches that are involved with each commits. 
					   You can also see the graph on github website under network.


In setting on github, you can set a branch as default branch. After that if you clone it, it will clone 
the default branch. 


Pull Conflicts:  
---------------
If the local changes and remote changes are different and conflicting. 

















