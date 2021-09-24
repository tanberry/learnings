# How internal team members can contribute to our  open source docs

## Contents

[Contributing](#contributing)

[Troubleshooting](#troubleshooting)

[Random notes of knowledge from Chris Nixon](random-notes-of-knowledge)

[Cherry Picking](#cherry-picking)

[Contributing to an existing PR branch](#contributing-to-an-existing-branch)

## Contributing

Anyone in our company, or out in our community, can help us improve our technical documentation that is in GitHub public repos. 

For suggestions, questions, etc you can open an Issue. 
For specific fixes with exact wording included, open a PR (pull request).

Below are the steps for setting up your own local working directory, and then committing your changes back to the upstream, original repository.

### Step 1. Setting up your local repo
1. Fork repo 
2. Clone repo
   1. In your terminal, create a new directory for the local repo using `mkdir <name-of-dir>`
   2. Initialize git in that directory using `git init`

6. Go to the upstream repo, and copy the URL for the repo, using the Clone button.

7. Then run: `git clone https://github.com/<repo name>`

8. Set remote as origin: `git remote add origin https://github.com/<repo name>`




### Step 2. Daily workflow

| Command      | Explanation |
| ----------- | ----------- |
| `git status`      | A quick check of current status of your local repo       |
| `git branch`   | Determine which branch you are in, locally        |
| `git switch master` |    |
| `git switch master` |  |
| `git pull origin` | Before synching with upstream’s /main, switch to your local /main branch and synch with it. This command synchs your repo with the upstream repo, so it will pick up any new changes by colleagues. A “git pull” is faster, but if you want to download only the meta-data about the changes, you can do git fetch, and then when ready to merge those changes,do a git merge. A “git pull” does a git fetch followed by a git merge |
| IF YOU ARE returning to a PR to work more on it after others have reviewed, requested edits, etc | Switch to your local branch, and run `git pull --rebase origin master`. This will apply any changes that have been made (to the upstream repo) on top of origin/master in your local branch. |
| Decide which branch to work in:

To create a new branch:
`git checkout -b <name of new branch>`

To switch to existing branch:
`git switch <name of branch>`
OR
`git checkout <name of branch>` | Typically you should name the working branch after the work ticket number or the task, to identify this particular chunk of work. |
git pull origin <branch name>


| `git branch` | To determine which branch you are currently in. Typically you want to work on a separate task-specific branch, not `/main`. |
| Do your coding, editing, writing work on the files usingvim or your fav editor
Keep your chunks of work relatively small and separate from other work. | Ideally, each branch that gets pushed is a single discrete chunk of work. This keeps you agile and able to more quickly commit completed work, or roll back sections. |
| `git add <name_of_file>` 
| `git commit -m “<your message enclosed in quotation marks>”`
| 'git push origin <branch name>` | When finished writing/editing, you need to  add, commit, and push the new file(s). 

Tips:
-- You can check which remote branch your local branch is tracking by running git status -sb. The top line will be the remote branch that git push defaults to. Or you can be explicit and do git push origin <branch name>
-- If there is not already a branch with the same name as your local working branch, this command will simultaneously create the upstream branch and push to it: `<your-branch-name>` |

## Step 3. Open a Pull Request
Go to the GitHub repository.
Go to the Pull Request “tab”.
Click the “Compare & pull request”button.





On the PR page, provide a commit message (or keep the one you added when committing). Also select at least two reviewers.
Click the Create pull request button.



Troubleshooting

Issue: If you get an error about credentials, look at the error message to see if it is trying to use https. If so, that won’t work cause we need to use SSH (to get around our SSO).
Solution: run `git remote set-url origin ssh://git@github.com:/logdna/logdna-agent-v2.git`

Random notes of knowledge from Chris Nixon
git has 3 “locations” on your machine, it has the working directory, ie your actual files on disk, the index which is the store where things that are waiting to be committed go, you “move” things from your working tree to the index using `git add`. The third place is the repository, you move things from the index to the repository using git commit
 
if you have already run `git add` but not yet `git commit` you can un-add. To “un-add” everything then you don’t need to provide a file name, if you only want to un-add a file you can give it the file name. For example, `git reset README.md`. And if you only want to un-add a “hunk” then you can do git reset --patch.
 
After running the `git reset <filename` command, the changed file will be unadded but it will still show as modified if you run `git status`. To fix that, run `git restore --patch`.
 
You can check which remote branch your local branch is tracking by running git status -sb. The top line will be the remote branch that git push defaults to. Else, yes, you can be explicit and do git push origin v2.2-docs-2 
 
ADDING TO AN EXISTING PR: If you clone the logdna/logdna-agent-v2 repo and check out my branch you can add changes to my PR. You just commit on top of the branch and push. Since the PR is just a diff of /master and v2.2, any changes you make to the branch v2.2 will get added to the existing PR.
 
if you do git push -u  it’ll automatically set the remote tracking branch to the same branch name as your local branch
 
Cherry Picking
git fetch
git checkout 3.0
git merge --ff origin/master
git checkout 2.2
git cherry-pick origin/master
 
Chris: “You’d need to checkout 3.2, then checkout -b a new, differently named docs branch, then run “git cherry-pick <name of your original docs branch>”
3:11
That would grab the commit with your changes without grabbing all of the changes from master.”
 
Contributing to an existing PR branch
 
If you want to make changes to the content in an open PR, follow these steps:
 
Synch with upstream:
On the /master, branch run git pull origin
Check out the PR’s branch: git switch <branch name>
Make your changes, save them.
Still in the PR’s branch, add your changes: git add <dir/file name>
Commit your changes: git commit -m <”message about change”>
Push your changes: git push origin <branch name>
 
DS_Store file mess:

Had an error where it complained about .DS_Store. Chris said to run:

git reset
git add docs/
 
This apparently “untracked the DS_Store file.

 
 
 

