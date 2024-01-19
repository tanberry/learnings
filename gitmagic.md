# Git Magic

## Contents

[Contributing](#contributing)

[Cheatsheets](#cheatsheets)

[Troubleshooting](#troubleshooting)

[Random notes of knowledge from Chris Nixon](#random-notes-of-knowledge)

[Cherry Picking](#cherry-picking)

[Contributing to an existing PR branch](#contributing-to-an-existing-branch)

[Using aliases](#using-aliases)

## Contributing

Below are the steps for setting up your own local working directory, and then committing your changes back to the upstream (official) repository.

NOTE: 
Think of the fork workflow as a triangle: you fork and clone the official repo, create a local copy, push that local copy to your fork, and then create a PR to pull in your updates TO the official repo FROM your fork.

![](./triangle.png)

### Step 1. Setting up your local repo
1. Fork the upstream repo (IF are an employee and have write access, just skip to Step 2 and clone the repo.)
2. Clone the forked repo in order to create a local working copy, using these commands:

   a. In your terminal, create a new directory for the local repo using `mkdir <name-of-dir>`.
   
   b. Initialize git in that directory using `git init`.
   
   c. Go to the upstream repo (your forked repo), click `< >Code` and then select **Clone** from the drop-down menu.
   
   d. Select HTTPs, and copy the URL for the repo, using the "copy" icon.
   
   e. Then in your terminal (inside the directory you just created), run: `git clone <the URL you copied>`

4. Define origin and upstream repos 

    a. Define origin: Set your remote repo (the forked one if you forked or or the official one if you only cloned) as origin: `git remote add origin https://github.com/<repo name>`.
    
    b. Define upstream: Set the upstream repo to point to the repo that you forked (or cloned): `git remote add upstream git://github.com/user/repo.git`.

Note: refer to this [great article](https://www.bogotobogo.com/DevOps/SCM/Git/GitHub_Fork_Clone_Origin_Upstream.php) to learn more about origin vs upstream.

### Step 2. Use one of the following processes, depending on if you **forked** the upstream repo or directly **cloned** it (usually the case if you are an employee and have write access).

#### Daily workflow with a **forked repo**

| Command      | Explanation |
| ----------- | ----------- |
| `git status`      | A quick check of current status of your local repo       |
| `git branch`   | Determine which branch you are in, locally     |
| `git switch main` |  move to the local main branch before  synching |
| `git pull origin main` | synch with the upstream repo every day BEFORE you begin your work. This command synchs your repo with the upstream repo, so it will pick up any new changes by colleagues. A “git pull” is faster, but if you want to download only the meta-data about the changes, you can do git fetch, and then when ready to merge those changes,do a git merge. A “git pull” does a git fetch followed by a git merge |
| IF YOU ARE returning to a PR to work more on it after others have reviewed, requested edits, etc | Switch to your local branch, and run `git pull --rebase origin main`. This will apply any changes that have been made (to the upstream repo) on top of origin/main in your local branch. |
| Decide which branch to work in: To create a new branch use `git checkout -b <name of new branch>`. To switch to existing branch use `git switch <name of branch>` OR `git checkout <name of branch>` | Typically you should name the working branch after the work ticket number or the task, to identify this particular chunk of work.|
| `git pull origin <branch name>` |   |
| `git branch` | To determine which branch you are currently in.  Typically you want to work on a separate task-specific branch, not `/main`.|
| Do your coding, editing, writing work on the files using vim, Atom, VSCode, or your fav editor. | Keep your chunks of work relatively small and separate from other work. Ideally, each branch that gets pushed is a single discrete chunk of work. This keeps you agile and able to more quickly commit completed work, or roll back sections. |
| `git add <name_of_file>` then `git commit -m “<your message enclosed in quotation marks>”` then 'git push origin <branch name>` | When finished writing/editing, you need to  add, commit, and push the new file(s). Tips:  -- You can check which remote branch your local branch is tracking by running `git status -sb`. The top line of the returned message is the remote branch that git push defaults to. Or you can be explicit and do `git push origin <branch name>`  -- If there is not already a branch with the same name as your local working branch, this command will simultaneously create the upstream branch and push to it: `<your-branch-name>` |

#### Daily workflow on a **cloned repo**

| Command      | Explanation |
| ----------- | ----------- |
| `git status`      | A quick check of current status of your local repo       |
| `git branch`   | Determine which branch you are in, locally.         |
| `git switch main` |  move to the local main branch before   |
| `git pull origin main` | synch with the upstream repo every day BEFORE you begin your work. This command synchs your repo with the upstream repo, so it will pick up any new changes by colleagues. A “git pull” is faster, but if you want to download only the meta-data about the changes, you can do git fetch, and then when ready to merge those changes,do a git merge. A “git pull” does a git fetch followed by a git merge |
| IF YOU ARE returning to a PR to work more on it after others have reviewed, requested edits, etc | Switch to your local branch, and run `git pull --rebase origin main`. This will apply any changes that have been made (to the upstream repo) on top of origin/main in your local branch. |
| Decide which branch to work in: To create a new branch use `git checkout -b <name of new branch>`. To switch to existing branch use `git switch <name of branch>` OR `git checkout <name of branch>` | Typically you should name the working branch after the work ticket number or the task, to identify this particular chunk of work.|
| `git pull origin <branch name>` |   |
| `git branch` | To determine which branch you are currently in.  Typically you want to work on a separate task-specific branch, not `/main`.|
| Do your coding, editing, writing work on the files using vim, Atom, VSCode, or your fav editor. | Keep your chunks of work relatively small and separate from other work. Ideally, each branch that gets pushed is a single discrete chunk of work. This keeps you agile and able to more quickly commit completed work, or roll back sections. |
| `git add <name_of_file>` then `git commit -m “<your message enclosed in quotation marks>”` then 'git push origin <branch name>` | When finished writing/editing, you need to  add, commit, and push the new file(s). Tips:  -- You can check which remote branch your local branch is tracking by running `git status -sb`. The top line of the returned message is the remote branch that git push defaults to. Or you can be explicit and do `git push origin <branch name>`  -- If there is not already a branch with the same name as your local working branch, this command will simultaneously create the upstream branch and push to it: `<your-branch-name>` |

### Step 3. Open a Pull Request
These steps assume that you ahve already pushed chnages to the upstream repo, so that when you go there, you see the request for the changes.

1. Go to the GitHub repository for the upstream repo (the official repo to which you want to contribute).
2. Go to the **Pull Request** tab. (There you should see a message about your recent push to the repo.)
3. Click the **Compare & pull request**.
4. On the PR page:
   a. provide a commit message (or keep the one you added when committing).
   b. change the commit title to match the directory destination for your changes. (Ex. `website/docs: commit message`.)
   c. select at least two reviewers.
6. Click  **Create pull request**.

## Cheatsheets
	
Here's a good [general overview](https://www.freecodecamp.org/news/git-cheat-sheet-and-best-practices-c6ce5321f52/) of common git commands.
	
### Concatenating Git commands:
	
From Jens: If you want to pull down a commit that was made in your PR upstream, and then run `make website` (for the linter), you can run `git pull; make website` and then commit the changes. (Assuming you’ve got the PR branch checked out, you can just run `git pull` and not specify theupstream branch.)

Use `;` to run commands one after another, `&&` to only run the next command if the first one is successful, and use `||` to only run the next command if the first one fails.

### Delete local branches

`git branch -d <local-branch>`
	
## Troubleshooting
	
### Synching your local `/main` to be exactly the same as upstream `/main` 
To get rid of unwanted changes and staged commits, run `git reset --hard origin/main`. To further cleanup, as in remove _DS_Store files, run `git clean -d -f`.

### Synching a local branch with the upstream `/main` 
If you created a local working branch, say `enterprise-docs` and you are working on it for weeks before you create the PR, you will want to update it in order to pull in all of the changes that have been made to the upstream `/main` branch. Otherwise, you wil have a ton of merge conflicts later when you create your PR and then try to merge it.

On your local working branch, run `git status` to make sure all of your local changes have been staged. If needed, run `git add` and `git commit` to stage the changes.

Now run `git fetch origin main`.

Finally run `git merge main`.

	
### Rebasing a remote branch/PR
	
For when you created a PR, then others make commits to it so that your local branch is no longer in synch with the remote branch of the PR. If a simple `git pull origin <remote-branch-name>` does not work, then Diane suggests this process: https://github.com/openedx/edx-platform/wiki/How-to-Rebase-a-Pull-Request.

However, I used this command (from [here](https://www.freecodecamp.org/news/error-failed-to-push-some-refs-to-how-to-fix-in-git/)) and it worked prefectly:

`git pull --rebase origin [branch]`

**Winner winner chicken dinner! -->** Jens recomended `git fetch --all` (which downloads all the upstream changes) and then `git reset --hard origin/*branch-name*` because it takes the remote changes and applies them.

From twitter, the suggestion to use `git restore —staged`. Removes the file from the Staging Area, but leaves its actual modifications untouched. By default, the git restore command will discard any local, uncommitted changes in the corresponding files and thereby restore their last committed state. With the --staged option, however, the file will only be removed from the Staging Area - but its actual modifications will remain untouched. ([source](https://www.git-tower.com/learn/git/commands/git-restore#:~:text=%2D%2Dstaged,restore%20their%20last%20committed%20state.))
	
### Removing files from a PR
If you accidentally included files (like random `.py` files, etc) that you do not want to include in the PR, use the following commands to remove them, delete them from commit, amend the commit message, and then force push to upstream branch.
	
Run `rm -r <dir-you-want-to-delete>` in the root source folder.
Then run `git rm -r <dir-you-want-to-delete>` and `git commit --amend` and finally `git push --force --set-upstream origin <name-of-PR-branch-on-remote>`.

### How to remove local untracked files from the current Git branch
* To remove directories, run `git clean -f -d` or git clean -fd. 
* To remove ignored files, run git clean -f -X or git clean -fX.
* To remove ignored and non-ignored files, run git clean -f -x or git clean -fx.

NOTES:
*   These commands only work if you `cd` into the actual dir where the untracked file is! However, you can run this one from the root: `git clean -f :/` (works as if you had run it in the root repo dir). 
   
### Personal tokens
	
Issue: if prompted for your password, you will need to use a "personal token" (post August 2021). For more info, refer to this [article](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 
   
### Credentials
	
Issue: If you get an error about credentials, look at the error message to see if it is trying to use https. If so, try using SSH (to get around our SSO).
Solution: run `git remote set-url origin ssh://git@github.com:/<company>/<repo>.git`
   
### Re-defining your origin or upstream repo:
* `git remote set-url origin <https:\\your repo url>`
* `git remote set-url upstream <https:\\your repo url>`
	
### DS_Store file mess:
	
On macOS systems, you often get extraneous files called .DS_Store. To unstage/untrack these files, run:

`git reset --hard HEAD && git clean -d -f`
 
Be aware that this will also unstage any pending files that were committed...  it will reset your local branch to be just like upstream branch. You should also add the file name to your gitignore file.

## Random notes of knowledge from Chris Nixon
* git has 3 “locations” on your machine, it has the working directory, ie your actual files on disk, the index which is the store where things that are waiting to be committed go, you “move” things from your working tree to the index using `git add`. The third place is the repository, you move things from the index to the repository using git commit
 
* if you have already run `git add` but not yet `git commit` you can un-add. To “un-add” everything then you don’t need to provide a file name, if you only want to un-add a file you can give it the file name. For example, `git reset README.md`. And if you only want to un-add a “hunk” then you can do git reset --patch. After running the `git reset <filename` command, the changed file will be unadded but it will still show as modified if you run `git status`. To fix that, run `git restore --patch`.
 
* You can check which remote branch your local branch is tracking by running git status -sb. The top line will be the remote branch that git push defaults to. Else, yes, you can be explicit and do git push origin v2.2-docs-2 
 
* if you do git push -u  it’ll automatically set the remote tracking branch to the same branch name as your local branch
 
* Cherry Picking
`git fetch`
`git checkout 3.0`
`git merge --ff origin/main`
`git checkout 2.2`
`git cherry-pick origin/main`
 
Chris re cherry-picking: “You’d need to checkout 3.2, then checkout -b a new, differently named docs branch, then run “git cherry-pick <name of your original docs branch>”. That would grab the commit with your changes without grabbing all of the changes from main.”

* ADDING TO AN EXISTING PR: If you clone the logdna/logdna-agent-v2 repo and check out another person's branch (i.e. (switch to that branch) you can add changes to their PR. You just commit on top of the branch and push. Since the PR is just a diff of /main and v2.2, any changes you make to the branch v2.2 will get added to the existing PR.
 
If you want to make changes to the content in an open PR, follow these steps:
 
1. Synch with upstream:
2. On the /main, branch run git pull origin
3. Check out the PR’s branch: git switch <branch name>
4. Make your changes, save them.
5. Still in the PR’s branch, add your changes: git add <dir/file name>
6. Commit your changes: git commit -m <”message about change”>
7. Push your changes: git push origin <branch name>

NOTE: recently, the final step above did not work for me, but rather created a brand new separate PR... instead of pushing my commits to the existing PR. The command that DID work is `git push <remote> <local_branch>:<remote_name>`

 ## How to manage upstream commits that are ahead of your local repo
   
 If you create a PR, and someone pushes commits to it upstream, you won't be able to do a `git pull` to synch. You will need to do a `git rebase` command.
   
  `git rebase origin <name of upstream branch>`
   
   
  For more info about using `rebase` see [How to Rebase a Pull Request](https://github.com/openedx/edx-platform/wiki/How-to-Rebase-a-Pull-Request).
	
## Alt text for images in blogs

`![Image1](./image1.jpg "Image by Joe")`

**Ken’s Better Way** (which still provides hover text, but also links the whole image.. so if a reader clicks on image, they go to the photographer’s website):

`[![Image1](./image1.jpg)](https://pixabay.com/users/jplenio-7645255/  "Image by jplenio on pixabay")`

## Using aliases
	
(Thanks to Ken @ authentik for this!)
	
#In your ~/.gitconfig file:
	
```	
[alias]
	
unstage = git reset -q HEAD --
	
nevermind = !git reset --hard HEAD && git clean -d -f
	
wip = for-each-ref --sort='authordate:iso8601' --format=' %(color:green)%(authordate:relative)%09%(color:white)%(refname:short)' refs/heads	
```
	
And an amazing list of aliases from Marc @authentik: https://gitlab.com/risson/soxincfg/-/blob/main/modules/programs/git.nix#L21
   
 
 

