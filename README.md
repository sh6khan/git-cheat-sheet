# git-cheat-sheet
This is my personal git cheat sheet. This is not a deep dive into how git works, just some of the simple stuff

# Contribute
Feel free to add or fix anything that you see. To contribute

- Fork the repo
- Clone the new forked repo into your local machine
- Create a new branch `git checkout -b your_contribution`
- After making your changes, `git commit -am 'small message about what you did'`
- Then push up into the remote repo with `git push origin HEAD`
- Go to GitHub, go to your forked repo and you should see a yellow bar mentioning your branch
- Go inside, scroll to the bottom and press on the `Make Pull Request` button
- I will get an email, notifying me of your Pull Request (PR) and if its good, I will merge it

# Overview
1. [Starting](#starting)
1. [Git Structure](#git-structure)
1. [Git Logs](#git-logs)
1. [Undo](#undo)
1. [Branches](#branches)
1. [Merging](#merging)
1. [Remotes](#remotes)
1. [GitHub](#github)
1. [Creating a Git Repo](#creating-a-git-repo)
1. [Git Clone](#git-clone)

## Starting
Starting is super easy... that is if you have a mac ! If you don't have a mac and are running Windows, then there is a very simple solution... Buy a mac !! (the new ones are like super thin)

open up your terminal to see exactly what version you have of git
```
$ git --version
git version 1.9.5 (Apple Git-50.3)
```
now that you are sure you have a working version of git, its time to create your working repository

go inside your project directory (in the terminal) and run `git init`, this will start git in keeping track of your changes
```
$ cd my_project
$ git init 
```
to verify, run `ls -al` and you should see `.git` file, that is how you know you have git for this directory. If you no longer want to use git on this dir, then simply delete the `.git` file.

## Git Structure
Git breaks things up into three 'trees' which are all maintained by git,

**Working Directory** : This is your current **local** tree. All the changes you make here will not affect anyone else 

**Staging** : or sometimes known as _index_ is - as the name implies - a staging tree. This is for keeping track of all the files that you changed

**HEAD** : A place that if in the future you make a mistake, you can revert/reset back to this current position. The **HEAD** always points to the most recent _commit_ but can point to earlier ones if you want. 

To move from one tree to another is simple
```
#this will move  files that you have made changes to into the staging getting ready for a commit 
#if you specify a file name, then only that file will be added to the staging tree and '.' will add all the files to staging
git add <filename> or git add .

#this will move from your Staging tree and create a commit, which you HEAD will now point to
git commit -m "commit message"

#you can do this all in online with
git commit -am "commit message"
```
There is a caveat to  using the last method there, If you created a brand new file, you have to first add it to _Staging_ with 
`git add <filename>`

## Git logs
the `git log` command is a great way to see all the commits that you have made, however it can be a little confusing and overwhelming
```
$ git log

commit cd62a7d33d8c20255ef4ba59da61ff21acbf903b
Author: sh6khan <sadman.khan999@gmail.com>
Date:   Fri Apr 3 03:14:41 2015 -0400

    one more method

commit 7b1db82140dc678eb869c742f0479ccf86168da5
Author: sh6khan <sadman.khan999@gmail.com>
Date:   Fri Apr 3 03:14:08 2015 -0400

    succesfull merges ?

commit bdc7ede1047a698955bd5b419de1ad9cada68b2c
Merge: 8bc63cf cb6ae5f
Author: sh6khan <sadman.khan999@gmail.com>
Date:   Fri Apr 3 03:12:54 2015 -0400

    Merge branch 'master' into random-branch
```
the large random assortment of numbers and letters right next to the word commit is the sha_key, it's a specific has value that references that particular commit 

- author is simple, its the user that made the commit

- date also very simple, the date of the commit 

- and finally the commit message. The commit message helps you understand what work you did with in that commit so make sure to make them as verbose as you can, especially if you are working with a team. 

There is one more thing that I should point out here. if the git log is large enough, git will open it in `vim`, an editor for the terminal. To exit the git log, simply press `q` after the `:`. so you will see this at the bottom of the page `:q`

But if you want cleaner more readable information, definitely try the following 
```
$ git log --pretty=oneline

184353d9f2b0df097bd0503bebabbe1c97925666 adding new methods for conflict
c0ca1332d8b1f631bd479d36286e08a5ae3ea004 deleting some methods
2846797d2bde3dc3bc09d8f3b77415eeb70693a1 Merge branch 'master' into random-branch
b2dba6730bee6badff97b992c301579559f4b039 conflict feature 2 on master
7221e6fcec75b293ba4679704a75daf6eaa87d8a branch conflict feature
9a99e3439256e70a6f6b0910597fbd2981bde9e5 added a conflict feature
f4a40bfd12a0e79bce3ae10292bd2bc5f6f1c4d9 fourth feature was added
```
To see all the commits made by one author. I will be using my `sh6khan` author name
```
$ git log --author=sh6khan
```
To see all your merges (We will talk about what a merge is later)
```
$ git log --merges
```
To see all your path of commits, with all it branches
```
git log --graph
```
to see all the other ways of viewing git logs you can checkout out the logs


## Undo
This is really the reason why we need git (for the cases where we make a mistake). But the problem there is many different ways to revert to an old commit based on the particular situation that you are currently in. 

I will be using the sha_key of 184353d9 as the commit key that we want to return to

##### Go back and checkout
1. there are no changes that have not been committed 
2. you just want to go back to older commit, but you don't want to delete all your newer commits

```
$ git checkout 184353d9
# or 
$ git checkout -b new_branch_name 184353d9
```

##### Delete everything and just start restart from chosen commit
1. there are no changes thay have not been committed
2. You made a mistake and just need to go back to that commit, erasing everything you have done since then 

```
$ git reset --hard  184353d9
```
##### Start over from head or master
1. you just made some changes to files for testing ( you do not want to commit )
2. you have not committed yet

```
$ git reset --hard HEAD
```
remember HEAD is a pointer to the latest commit on that branch

##### Ctrl + Z

1. You have no idea what you did, no idea where you are and you just want to go back

- The reflog is the ultimate safety net. It keeps track of everything you just did, from checking out new branches, to rebases, the reflog is the essentialy a way to move back through time 


```
$ git reflog

# after finding the place you want to go back to 

$ git reset --hard <sha_key>
```

## Branches
the Master branch is the branch that you start in and its the branch that you should never work directly on. Anytime you want to make a change or add a feature, you should checkout a different branch. Once you have finished implementing said feature you can then merge your branch into master. This is great because it allows you to organize your features and keep a controlled working version of the app to compare with.

Branches are a great way to start implementing new features. When you start making a new feature, you first run `git pull` on the master branch to make sure you have all the latest code.

- You should never be getting a merge error when doing a `git_pull`. If you find your self in this situation that means that you made a few commits on the master branch by accident. Stop the merge and make sure you're on a clean tree, then do this:

	```
	$ git checkout -b temp-changes
	$ git reset --hard origin/master
	```
- all your changes that should not have been on master has no been moved to a separate branch (temp-changes). the second line then looks at the remote directory and just sets your local master to the same one that is in origin (origin is the name of the remote branch).

To create a new branch 
```
$ git checkout -b new_branch_name
```
branch names should be descriptive to what you are trying to do. They cannot have any spaces in the names and its most common to use either `-` or `_` to separate the words

```
$ git checkout -b getting-live-messages-from-websocket
```
To see which branch you are currently in 

```
$ git status
#or 
$ git branch
```
To merge a branch once you are done. We will be merging the `getting-live-messages-from-websocket` branch _into_ master

```
$ git checkout master
$ git merge getting-live-messages-from-websocket
```
## Merging 

##### Merge 
```
$ git merge branch_name
```

* When merging, you are usually on the master branch and merge with your own branch

##### Rebase 

* When rebasing, you are usually on the branch you are working on.
* Rebase right before you decide merge with master

```
$ git rebase master
```
_Why Rebase?_, It's a great to make a clean looking tree, it appears as if you never created a branch to begin with. Remember a rebase is simply shifting the commit that your branch branched off of, to be the HEAD of master

#Merge Conflicts

If you try and to do a merge, there is likely chance that you will end up with a merge conflict. Before we go over how to solve these problems, an important thing to learn is how to back out of the current predicament

```
$ git merge --abort
# or 
$ git rebase --abort
```
To see which files contain merge conflicts. Just run

```
$ git status
```
The important thing to remember here is that you have final say as to how the merge conflict is handled. If a coworkers spent hours and days on a feature that conflicted with yours, You can simply over write all their hard work. (But lets try our best to be not be so selfish ;) )

##### Edit Conflicts
* Most common, two people have edited the same file. 

```
<<<<<<< HEAD
def function_one
=======
def function_two
>>>>>>> your_branch
```
`your_branch` is the name of the branch that you are merging, `HEAD` is the latest commit on the branch that you are merging with. Going back to our example, `HEAD` would be the _HEAD_ of the master branch

then do 
```
$ git add .
$ git commit -am "fixing merge conflicts"
```

* If you want to simple take the changes that are in `HEAD`

```
$ git checkout --theirs <file_name_that_has_merge_conflict>
```

* If you want to keep your own changes

```
$ git checkout --yours <file_name_that_has_merge_conflict>
```

##### Removed files conflict 
* One person modified to the file, while another deleted the file

you actually have two choices here, delete the file , or keep the changes

1. keeping the file with new changes

Simply add the file back and commit. (lets say the README.md file was modified)

```
$ git add README.md 
$ git commit 
```

2. deleting the file and disregarding the changes

simply remove the file and commit 

```
$ git rm REAMDE.md 
$ git commit
```

If you had a conflict in the middle of a rebase, after fixing your conflicts run:

```
git add .
git rebase --continue
```

## Remotes

We are nearing the section of GITHUB so it's time to introduce **Remotes**

- When you use `git init` you just started git version control on that local directory (and child directory). But everything is maintained in your local machine. The concept of a remote is to start keeping version on github's repository

- First you have to actually create the remote repository, which is very simple to do. Just go on Github.com and click the `New Repository` icon the nav bar

- Github will give you all the needed instructions as to how we move our project into the remote repo 

- By default the name of your repo and all remote repo's are set to **origin**. Note that you never have to change this if you don't want to (most preople don't) 

##### Push

- To push a new branch onto the remote repo

	```
	$ git push -u <remote\_repo_name> <branch_name>
	```

- Or to make things a little nicer 

	```
	$ git push -u origin HEAD
	```
- Even nicer, if you change the settings in your gitconfig

	```
	$ git push 
	```
- This will push the current branch that you are working on 

The `-u` is short for `--set-upstream`, which just means that if you ever want to `pull` the remote branch, you simply have to type 
`git pull` while you are currently checked out in the local branch


## GitHub

Github is a website that anyone can access and a great way to work on projects with other people. You can also use Github to contribute to open source, a great way to help everyone!

## Creating a Git Repo

- Go to the top right of the page and click on the create new button. Then pick `New repository`. 
- pick the name of the repo, the name should be the name fo the project that you are working on. For example the name of this repo is
**git-cheat-sheet**

- You want initialize with a README.md file. The README.md is a file that you want other people to read before looking at your project
For example, what you are reading right now is a README.md file. If you want to learn about mark down, which is how you can make cool things on your docs go here: https://help.github.com/articles/github-flavored-markdown/

- And thats all! You have just created your remote repository. If you have an existing projects, you can import that project to this repo. If this is just the beginning, you can clone the remote repo to your local machine. 

## Git Clone

- If you look on the right side of home page in a git repo, you will see this _git clone_ clink. Copy that link to your clipboard, either with just `cmd + v` or just clicking on the clipboard icon. Then go to the directory where you want to add the project and run 

```
$ git clone <clone_link>

# example

$ git clone https://github.com/sh6khan/git-cheat-sheet.git
```





