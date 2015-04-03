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
>> git version 1.9.5 (Apple Git-50.3)
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
#if you specifiy a file name, then only that file will be added to the _staging_ tree and . will add files to  _staging_
git add <filename> or git add .

#this will move from your Staging tree and create a commit, which you HEAD will now point to
git commit -m "commit message"

#you can do this all in online with
git commit -am "commit message"
```
There is a caviat to  using the last method there, If you created a brand new file, you have to first add it to _Staging_ with 
`git add <filename>`

#Revert Reset
This is really the reason why we need git (for the cases where we make a mistake). But the problem there is many different ways to revert to an old commit based on the perticular situation that you are currently in. 





