# GIT Command Line

**Table of Contents**
- [Branch](#branch)
- [Commit](#commit)
- [Tag](#tag)
- [Tips](#tips)

-------------

### Branch
- ##### Create branch
  Local  
  `$ git branch checkout -b <new-branch-name>`  
  Remote  
  `$ git push -u origin <new-branch-name>`  
- ##### Rename branch
  `$ git branch -m <new-branch-name>`  
  `$ git push -u origin <new-branch-name>`  
- ##### Remove branch
  Local  
  `$ git branch -D <branch-name>`  
  Remote  
  `$ git push origin --delete <branch-name>`  
- ##### Remove multiple branch
  Local  
  `$ git branch -D <branch-name> <branch-name>`  
  `$ git branch -D $(git branch | grep develop/*)`  
  Remote  
  `$ git push origin --delete {branch-name} {branch-name}`  
  `$ git branch -r | awk -F/ '/\/PREFIX/{print $2}' | xargs -I {} git push origin :{}`  
- ##### Remove All Local Branches not on Remote
  `$ git branch -r | egrep -v -f /dev/fd/0  <(git branch -vv | grep origin) | xargs git branch -d`
- ##### Delete All Your Local Git Branches Except Master
  `$ git branch | grep -v "master" | xargs git branch -D`

### Commit
- ##### Comit all change and message
  `$ git commit -am "commit message"`
- ##### Edit message after commit pushed (latest)
  `$ git commit --amend -m "New commit message."`

### Tag
- ##### Add
	`$ git tag <tag name>`  
	`$ git push origin <tag name>`  
- ##### Remove
	`$ git tag --delete <tag name>`  
	`$ git push origin :<tag name>`  
- ##### Clear Tag Local and Fetch Remote
	`$ git tag -l | xargs git tag -d`  
	`$ git fetch -t`  

### Tips
- ##### Merge multiple commit to single commit
	- 2 commit  
	`$ git reset --soft "HEAD^"`  
	`$ git commit --amend`  

	- 10 commit  
	`$ git reset --soft "HEAD~10"`  
	`$ git commit --amend`  
- ##### Undo pushed commit
	- New commit  
	`$ git revert <commit_hash>`  
	`$ git revert <oldest_commit_hash>..<latest_commit_hash>`  

	- Without new commit  
	`$ git push -f origin <last_known_good_commit>:<branch_name>`  
	`$ git reset --hard <last_known_good_commit>`  
- ##### Rebase checkout commit onto another commit  
	`$ git rebase -i <sha_commit>`  
- ##### Discard Change  
	`$ git checkout -- .`  

