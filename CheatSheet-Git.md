## Purpose: Remind myself of the Useful Git Commands

&nbsp;
&nbsp;

### Git Commands
| Commands | Meaning | Resources |
| :--- | :--- | :---: |
| `git init`  | initialize a local git repository | 
| `git add .` | add all the files that were changed since the last back up or commit to the staging area |  |
| `git add <fileNameWith.extension>` | add the specified file to staging *before* running `git commit` |  |
| `git commit -m "..." ` | commits the changes to the local git repository |  |
| `git remote add origin https://---.git` | tells git to add a remote repo (origin: GitHub or GitLab or BitBucket) with the provided URL location  <br> `git remote add origin https://github.com/<gitub_Username>/<github_Repo_Name>.git` <br>`git remote add origin https://github.com/geeeedev/sandbox-react.git` |  |
| | | |
| `git push` | push the changes to the remote repository from your local repository <br> `git push origin` &nbsp;&nbsp;&nbsp;//origin = GitHub repo  <br> `git push origin master` &nbsp;&nbsp;&nbsp;//master = local repo |  |
| `git push --all ` | push all branches to remote repository <br> `git push --all origin`  |  |
| `git pull` | pull the changes from the connected remote repository to your current local directory |  |
| `git status` | shows all the files that were changed since the last backup and which ones are already added to the staging area |  |
| `git status <branchName>` | shows all the files that were changed since the last backup and which ones are already added to the staging area |  |
| | | |
| `git checkout -b <branchName> <optionalFromBranch>` | switches to the branch name provided in local git repository.  <br>will create a new branch *and* switch to it if the branch name provided does not exist.  <br>this replaces below git branch and git switch two steps| [learn more](https://www.atlassian.com/git/tutorials/using-branches) |
| `git branch <branchName>` | creates a new branch using branch name only - does *not* switch over to the newly created branch | [learn more](https://www.atlassian.com/git/tutorials/using-branches) |
| `git checkout <branchName>` | switches over to the provided branch name | [learn more](https://www.atlassian.com/git/tutorials/using-branches) |
| `git checkout -` | quick switches between last two working branches | [learn more](https://medium.com/@gitship/15-git-hacks-to-save-your-life-as-a-developer-aa8808846dbb) |
| `git branch` | shows all of your git branches and marks the one you are currently on in green | [learn more](https://www.atlassian.com/git/tutorials/using-branches) |
| `git merge <branchName>` | merges provided branch name to existing (main) branch - be sure to `checkout` and switch over to the main branch first  | [learn more](https://www.atlassian.com/git/tutorials/using-branches) |
| `git diff` | view all merge conflicts (when conflict occurs after git merge) |  |
| `git diff --base` | view merge conflicts against the base file |  |
| `git branch -d <branchName>` | deletes the provided branch name *with safe operation* to prevent deletion when unmerged changes exist |  |
| `git branch -D <branchName>` | *FORCE* deletes the provided branch name regardless of unmerged changes existence  |  |
| | | |
| `git log` | shows all the backups created in the repository <br> type 'q' to exit log |  |
| `git clone <url>` | clones a remote repository from the provided URL to your current local folder directory <br> `git clone https://github.com/geeeedev/chittychat.git` |  |
| `git fetch` | ... ... ... ??? ??? |  |
| `git stash` | ... ... ... ??? ??? |  |
| `git tag`   | ... ... ... ??? ??? |  |
| | | |
| `git remote remove <remoteRepoName>` | delete remote repo you added |  |
| `git remote` | list all remote repos you are connected to |  |
| `git remote show <remoteRepoName>` | see more info about a remote repo <br> `git remote show origin` |  |
| `git remote get-url origin` | list the URL address of the remote repo (origin) |  |
| `git blame <filePath/filePath/fileName.ext>` | shows who wrote which line of code with timestamp, in other words who is to be blamed for that particular line of code |  |
| | | |  

![](./Screenshots/git-Commands.png)

&nbsp;
&nbsp;

### Git Config
| Commands | Meaning |
| :--- | :--- |
| `git config --global user.name "..."` | set username |
| `git config --global user.email xxxxxx@xxxx.xxx` | set email |
| `git config --global --list` | list and verify settings |
| `git config --global color.ui "auto"` | turn on color codes in Git output in Terminal |
| | | |

![](./Screenshots/git-Config.png)  

> [See more helpful shortcuts](https://medium.com/@gitship/15-git-hacks-to-save-your-life-as-a-developer-aa8808846dbb)

