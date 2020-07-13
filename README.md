# GIT
Learn GIT
https://git-scm.com/

Check if git is installed
$ git version
git version 2.27.0.windows.1
(if something is wrote about GIT version it's mean that git is installed)

## Adding repository from GitHub

1. pwd - check user's home directory
$ pwd
/c/Users/nn

2. mkdir - create directory 'projects'
nn@DESKTOP-6PNIKK1 MINGW64 ~
$ mkdir projects

3. cd - going repository

nn@DESKTOP-6PNIKK1 MINGW64 ~
$ cd projects

nn@DESKTOP-6PNIKK1 MINGW64 ~/projects
$ pwd
/c/Users/nn/projects

$ git config --global user.name "NAME"
$ git config --global user.email "EMAIL"

$ git config --global --list
user.name=NAME
user.email=EMAIL

$ git clone https://github.com/testerBartek/GIT

Cloning into 'GIT'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 613 bytes | 68.00 KiB/s, done.


$ ls (list what is in this directory)


https://stackoverflow.com/questions/48012838/hide-username-and-computer-name-from-git-bash-for-windows-10
Follow the steps below:
Go to C:\Program Files\Git\etc\profile.d\ folder
Find and open git-prompt.sh file in your favorite text editor
Go to line number 15
Replace the whole line with PS1="$PS1"''
That's it. Start/Restart Git Bash and you should see the username and computer name is gone.
NOTE: You can also hide the annoying MINGW64 text by commenting out the line number 16 and 17 of the same file. To comment out those lines just add a # to the beginning of the line. That's it. Now start/restart Git Bash and it should go away.

$ git status 

$ clear

~/projects/GIT (master)
$ echo "Test Git Start" >> start.txt

~/projects/GIT (master)
$ ls
README.md  start.txt

~/projects/GIT (master)
$ cat start.txt
Test Git Start

~/projects/GIT (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        start.txt

no changes added to commit (use "git add" and/or "git commit -a")

~/projects/GIT (master)
$ git add start.txt

~/projects/GIT (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   start.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md


~/projects/GIT (master)
$ git commit -m "Adding start text file"
[master 221b7f7] Adding start text file
 1 file changed, 1 insertion(+)
 create mode 100644 start.txt

~/projects/GIT (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

~/projects/GIT (master)
$ git push origin master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 303 bytes | 151.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/testerBartek/GIT
   02277b3..221b7f7  master -> master

   
