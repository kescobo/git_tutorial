# Git Boot Camp
**Led by Kevin Bonham, PhD**

_Wednesday, June 6 2018_

_10:30 AM - ? PM_

_SCI 143_

## Set Up

1. [Git](https://git-scm.com/)
2. Python
    * Mac already has a system version of Python
    * To check version ...
3. [Homebrew](brew.sh)

    `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

4. Jupyter lab

    `$ brew install jupyter`

    `$ brew install python 2`

    `$ brew install python 3`

5. Biobakery
  * Metaphlan2
  * humann2
6. Text editor
  * [Atom](https://atom.io/)
  * [Sublime Text](https://www.sublimetext.com/)
  * [textwrangler](https://www.barebones.com/products/textwrangler/download.html) *not compatible with Mac OS 10.13 (High Sierra)*


## What is Git?
 **Git** = distributed version control system (dvcs)

 Allows you to keep track of the state of an entire folder

 **Repo** = folder, abbrev. repository

 **Commit** = snapshot of folder state

* git_tutorial-1/
  * notes/
    * sophie.md
    * danielle.md
    * kevin.md
  * bin/
    * myscript.py

_git_tutorial-1 because previously made git_tutorial_

### Organization of Repos
1. Local = own copy on your computer
2. Remote = another place to store files, like GitHub
3. Remote (upstream) = *Source of Truth*, main lab repo

## Terminal Tutorial
* Preview working directory = `$ pwd`
* Change directory = `$ cd {folder}/`
* Make directory  = `$ mkdir {new_folder}/`
* List files in directory = `$ ls` OR `$ ls -a`
* Remove folder = `rm -r git_tutorial` OR `rm -rf git_tutorial`
  * Use **sparingly**

### Create a remote repo
**_Don't do yet_**
`$ git remote add origin git@github.com:kescobo/git_tutorial.git`

## Create README.md file
`$ atom README.md`

*If using Atom text editor*

You created a new text file (.md = markdown)! You can save like a normal file but need to commit to add to local repo and push to remote repos.

Atom tracks your file status
* Green = not tracked by Git
* Yellow = tracked, but most recent version not committed

## Important Git Commands
* Create new repo = `$ git init {new_repo}/`
* Check status of local repo = `$ git status`
* Stage files = `$ git add {new_folder}/{filename}`
* Commit files = `$ git commit -m "Enter commit message here"`
    * `-m` = add message
* Push & set upstream = `$ git push --set-upstream origin master`
    * Push = `$ git push`
    * `origin master` = <remote repo name> <branch name>
* View commit history = `$ git log`
    * To make it look pretty `$ git log --graph --pretty=oneline --abbrev-commit`
* Create new branch = `$ git checkout -b {new_branch}`
* Check status of remote repo = `$ git fetch`
* Update local repo from remote repo = `$ git pull`
    * Specify which remote repo to pull from
* Set another remote repo = '$ git remote add upstream https://github.com/kescobo/git_tutorial.git'
    * "upstream" = repo name
    * https:// = url from clone or download on GitHub
* Pull from remote = `$ git pull`
    * Default pulls from "origin"
    * `$ git pull upstream master`
    * **Double-check** which branch you are on
* Make master branch match dev = `$ git checkout sophdev`
    `$ git merge master`

OR

* Make dev branch match master = `$ git checkout master`
    `$ git merge sophdev`

### Copy repo
1. Fork from origin on GitHub
2. Clone onto your computer
  * `git clone {insert url here}`

## General Work Flow
1. Make a branch  
      `$ git checkout -b {new_branch}`
2. Commit to branch  
      `$ git add {filename}`
      `$ git commit -m "Commit message"`
      `$ git push --set-upstream origin sophdev`
3. Pull request to upstream
        * Submit pull request on GitHub
        * Address comments
        * Commit and push any changes
        * **Do not merge yourself!** Kevin is in charge of merging pull request to upstream
    1. When merged, pull from upstream (_while in master branch_)  
        `$ git checkout master`  
        `$ git pull upstream master`
    2. Merge sophdev to master  
        `$ git checkout master`  
        `$ git merge sophdev`  
        *If doesn't work, switch sophdev and master*
