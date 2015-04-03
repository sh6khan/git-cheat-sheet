# git-cheat-sheet
This is my personal git cheat sheet. This is not a deep dive into how git works, just some of the simple stuff

#Contribute
Feel free to add onto this little guide if you just happed to find the next big trick with GIT, I know myself and many others who are very confused about git could definetly use the help! :)

#GIT and GITHUB
Im am going to break this into two sections, one is GIT version control and the other is GITHUB. I find that the two are different enought that they each warrent seperate sections. for the first section we will simply be talking about all the ways that you can use GIT to version control your app, so that if you ever make a mistake everything will still be all good. The second section on GITHUB will be more on how to fork repos , and contribute to other repos. I will also be talking about the ways that you review other peoples code and how to make pull requests

#Starting
Starting is super eazy... that is if you have a mac ! If you dont have a mac and are running Windows, then there is a very simple solution... Buy a mac !! (the new ones are like super thin)

open up your terminal to see exactly what version you have of git with
```
$git --version
git version 1.9.5 (Apple Git-50.3)
```
now that you are sure you have a working version of git, its time to create your working repositiory

go inside your project directory (in the terminal) and run `git init`, this will start git in keeping track of your changes
```
$ cd my_project
$ git init 
```
to verify run `ls -al` and you should see `.git` file, that is how you know you have git for this directory. If you no longer want to use git on thid dir, then simple delete the .git file

#GIT Structure
GIT breaks things up into three 'trees' which are all maintained by git,

**Working Directory** : This is your current **local**(you'll be seeing that world alot) tree. All the changes you make here will not affect anyone else 

**Staging** : or sometimes other wise known as _index_ is as the name indicates a staging tree. This is for keeping track of all the files that you changed

**HEAD** : this to me is a checko point, like in a video game. A place that if in the future you make  mistake, you can revert/reset back to this current position. the **HEAD** always points to the most recent _commit_ but can point to earlier ones if you want 

To move from one tree to another is simple
```
#this will move  files that you have made changes to into the staging getting ready for a commit 
#if you specifiy a file name, then only that file will be added to the staging tree and '.' will add all the files to staging
git add <filename> or git add .

#this will move from your Staging tree and create a commit, which you HEAD will now point to
git commit -m "commit message"

#you can do this all in online with
git commit -am "commit message"
```
There is a caviat to  using the last method there, If you created a brand new file, you have to first add it to _Staging_ with 
`git add <filename>`

#GIT logs
the `git log` command is a great way to see all the commits that you have made, however it can be a little confusing and overwhelmging
```
$ git log

commit cd62a7d33d8c20255ef4ba59da61ff21acbf903b
Author: sh6khan <sadman.khan999@gmail.com>
Date:   Fri Apr 3 03:14:41 2015 -0400

    one more method

commit 7b1db82140dc678eb869c742f0479ccf86168da5
Author: sh6khan <sadman.khan999@gmail.com>
Date:   Fri Apr 3 03:14:08 2015 -0400

    successfull merges ?

commit bdc7ede1047a698955bd5b419de1ad9cada68b2c
Merge: 8bc63cf cb6ae5f
Author: sh6khan <sadman.khan999@gmail.com>
Date:   Fri Apr 3 03:12:54 2015 -0400

    Merge branch 'master' into random-branch
```
the large random assoirmand of numbers and letters right next to the word commit is the sha_key, it's a specific has value that refrences that perticular commit 

author is simple, its the user that made the commit

date also very simple, the date of the commit 

and finally the commit message. The commit message helps you understand what work you did with in that commit so make sure to make them as verbose as you can, especially if you are working with a team. 

There is one more thing that I should point out here. if the git log is large enough, git will open it in `vim`, an editor for the terminal. To exit the git log, simply press `q` after the `:`. so you will see this at the bottom of the page `:q`

But if you want cleaner more readable information, definitly try the following 
```
$ git log --pretty=oneline

184353d9f2b0df097bd0503bebabbe1c97925666 adding new methods for conflict
c0ca1332d8b1f631bd479d36286e08a5ae3ea004 deleteing some methods
2846797d2bde3dc3bc09d8f3b77415eeb70693a1 Merge branch 'master' into random-branch
b2dba6730bee6badff97b992c301579559f4b039 confict feature 2 on master
7221e6fcec75b293ba4679704a75daf6eaa87d8a branch conflict feature
9a99e3439256e70a6f6b0910597fbd2981bde9e5 added a conflict feature
f4a40bfd12a0e79bce3ae10292bd2bc5f6f1c4d9 fourth feature was added
```
To see all the commits made by one author. I will be using my person `sh6khan` author name
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


#Undoing things
This is really the reason why we need git (for the cases where we make a mistake). But the problem there is many different ways to revert to an old commit based on the perticular situation that you are currently in. 





