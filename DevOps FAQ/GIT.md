### 1. What is Version Controlling?
Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. It allows multiple people to collaborate on the same files, and helps to resolve conflicts when multiple people make changes to the same files simultaneously.
There are many different version control systems, but the most popular one is git, which was created by Linus Torvalds in 2005. Git is a distributed version control system, which means that each person who works on the project has a copy of the entire repository (i.e., the set of files and directories) on their own computer. This allows them to work independently and then to push their changes to a central repository when they are ready to share them.
GitHub is a web-based platform that uses git as the version control system and provides a way for developers to store, collaborate and share their code.

### 2. What is the usual workflow using VCS?
The usual workflow for using a version control system (VCS) like git typically involves the following steps:
1. Cloning: To start working on a project, you will first need to clone (or copy) the repository from a remote server to your local machine.
2. Making changes: After you have a local copy of the repository, you can begin making changes to the files. This can include adding new files, modifying existing files, or deleting files.
3. Committing: Once you've made some changes, you will want to save a snapshot of your work in the form of a commit. A commit is a snapshot of your repository at a specific point in time, and it includes a message describing the changes you made.
4. Pushing: Once you have committed your changes, you will likely want to share them with others. You can do this by pushing your commits to a remote repository. This will make your changes available to other people who are working on the same project.
5. Pulling: Before you start making any changes, it's always a good idea to check if there are any updates from other people that you need to incorporate into your local repository. You can do this by pulling the changes from the remote repository to your local machine.
6. Branching: One of the most important feature of VCS like git, is the ability to work in parallel with other developers by creating branches, which allows multiple people to work on the same project without interfering with each other. Once you are done with your work and your branch is ready, you can merge it back to the main branch.

It's worth to mention that, not all projects are the same and this workflow can vary depending on the project and the organization but git's branching model makes it very flexible to adapt to different needs.

### 2. What is the usual Checkout using Checkin?
Checkout and checkin are terms commonly used in version control systems (VCS) to refer to the process of taking and returning files for editing.

The usual process of "checking out" a file involves:
1. Selecting the file or files you want to work on
2. Retrieving a copy of the file from the version control repository to your local machine
3. Marking the file as "checked out" in the version control system so that others know that you are currently working on it

Once you've made your changes to the file, you would then "check it in" which typically involves:
1. Saving the file to your local machine
2. Updating the version control repository with your changes
3. Marking the file as "checked in" in the version control system so that others know that it's now available for them to work on.
4. When multiple people are working on the same project, the process of checking out and checking in is an essential way to prevent conflicts and ensure that everyone has the most up-to-date version of the files.

It is important to note that different VCS have different workflow and terminology but the concept of locking or marking files as being in use by someone else is present in most of them.

#### 4. What are different types of VCs available?
There are several different types of version control systems (VCS) available, each with its own unique features and characteristics. Some of the most popular types include:

1. Centralized version control systems (CVCS) are based on a central repository where all files and revisions are stored. All developers access the same repository, with read and write permissions controlled by the administrator. Examples of CVCS include Subversion (SVN) and Perforce.
2. Distributed version control systems (DVCS) are based on a distributed model, where each developer has a complete copy of the repository on their local machine. This allows developers to work independently, and then to merge their changes with the main repository when they are ready to share them. Examples of DVCS include Git and Mercurial.
3. Lock-modify-unlock systems systems are based on the concept of 'locking' a file before editing it, and 'unlocking' it after the change has been made. This prevents multiple people from making changes to the same file at the same time, but it can also lead to conflicts. Examples of this type of VCS include VSS and PVCS.
4. File-system based version control systems are those that monitors file system changes in a specific folder or tree structure and records those changes, which allows to revert or compare changes but lack advanced features like branching and merging. Examples include Microsoft's built-in Previous Versions feature and Time Machine on Mac OS.

### 5. How to install Git on Windows?

1 Open https://git-scm.com/downloads
2 Download git for windows
3 Install it
4 Once git is installed we get an application called gitbash
  where we can fire the git commands

### 6. How to install Git on Ubuntu?

1 Connect to a ubuntu linux
2 Update the apt repository
  sudo apt-get update
3 Install git
  sudo apt-get install -y git

### 7. How to install Git on RHEL,Centos,Fedora?

1 Update the yum repository
  yum -y update
2 Install git
  yum install -y git

### 8. How to setup and list username and email for all users for Git?

git config --global user.name "sai krishna"
git config --global user.email "intelliqittrainings@gmail.com

To see the list of configurations done
git config --global  --list

### 9. What are the sections Git uses when working on the local machine?
When working with Git on a local machine, there are three main sections that are used to store and manage the files:

1. The Working Directory: This is the area where you will make changes to the files on your local machine. When you first clone a repository, the files in the working directory will be the same as the ones in the repository. As you make changes, the files in the working directory will become different from the ones in the repository.
2. The Staging Area: The Staging Area (also called the index) is an intermediate area where you can prepare your changes before committing them to the repository. When you add changes to the Staging Area, they are ready to be committed, but they are not yet saved in the repository. This allows you to review your changes and make sure they are correct before committing them.
3. The Repository: The repository is the final destination of your changes, it's where all the commits are stored. This is where the permanent and historical record of your work is kept. The repository contains the entire history of your project and can be used to revert to previous versions of the files or compare different versions.

To better understand the workflow, it's common to visualize this as a pipeline, where changes go from the working directory, through the staging area, and then are committed to the repository.
Additionally, git have another section called 'Remote' which is used to connect to a remote repository and synchronize changes between local and remote repository.

### 10. How connect to a remote repository and synchronize changes between local and remote repository?

1. Push changes to the remote repository: After you have committed your changes, you can push them to the remote repository. This will make your changes available to other people who are working on the same project.
```
git push origin master
```
The git push command pushes commits from the local repository to the remote repository. In this example, the origin is the name of the remote repository, and master is the name of the branch being pushed.

2. Pull changes from the remote repository: When other people make changes to the remote repository, you'll want to pull those changes into your local repository to stay up to date.
```
git pull origin master
```
The git pull command fetches changes from the remote repository and merges them with the local repository. In this example, the origin is the name of the remote repository, and master is the name of the branch being pulled.

### 11. Give sample workflow that Git can be used to demonstrate sections?

1. To initilise the current folder as a git repo
```
git init
```
This command will create a hidden folder called as ".git" where it stores all the configurations related to git/
2. To send a files from working directory to stagging area
```
git add filename
```
b. To send multiple files to stagging area
```
git add file1 file2 file3
```
c.  To send all the files and folders from working dir to staggingarea
```
git add .
```
3. To send the files from stagging area back to working directory
```
git rm --cached filename
```
or
```
git reset filename
```
4. To send files from stagging area to local repository
```
git commit -m "Some message"
```
5. To see the status of untracked and staged files
```
git status
```
6. To see the list of versions i.e, logs sent into local reposiotory
```
git log
```

### 12. What is the different between rm --cached and reset?
git rm and git reset are two different commands in Git that are used for different purposes.

1. git rm is used to remove files from the Git repository. The --cached option allows you to remove a file from the repository without deleting it from the file system. This is useful if you want to stop tracking a file without deleting it from your project. When you use git rm --cached, the file is removed from the repository and the next commit will not include that file, however, the file still exists on your local machine.
```
git rm --cached file.txt
```
2. git reset, on the other hand, is used to undo changes that have been made to the repository. It can be used to reset the state of the repository to a specific commit, or to unstage changes that have been added to the staging area but not yet committed.
```
git reset file.txt
```
This command will unstage the file and make it ready for a new commit, however, it doesn't delete the file from the file system or from the repository, it just undo changes made to it.

In summary, git rm --cached is used to stop tracking files in Git, while git reset is used to undo changes that have been made to the repository.

### 13. What is .gitignore?
.gitignore is a file in a Git repository that tells Git which files or directories it should ignore and not track. This is useful if you have certain files or directories that you don't want to include in the repository, such as build artifacts, compiled binaries, or sensitive information.

The .gitignore file is usually located at the root of the repository, and it should be added and committed to the repository like any other file. The file should contain a list of file and directory patterns, one per line, that Git should ignore.
The most common use of .gitignore is to ignore files that are generated by your build process, or files that contain sensitive information.

It's worth noting that the ignore rules set in the .gitignore file will apply to all branches in a repository and it's not only for the current branch but all branches. Also, files that are already tracked by Git are not affected by changes to .gitignore, if you want to stop tracking a file that is already being tracked, you can use git rm --cached.

### 13. Demonstrate an example with .gitignore?
1. Create few files
```  
touch f1 f2 f3 f4 f5
```
2. Check the status of git
```
git status
```
This will show the above 5 files as untracked files.
3. Create .gitignore and store the above 5 file names in it
```  
cat > .gitignore
f1
f2
f3
f4
f5
```
To come out of cat command press ctrl+d  
4. Check the status of git
```  
git status
```  
This will only show .gitignore as untracked, f1-f5 are no longer accessable by git.

### 14. What is branching in Git?

Branching in Git is a feature that allows you to work on multiple versions of your code at the same time. When you create a new branch, you are creating a copy of the code at that point in time, and any changes you make to the code in that branch do not affect the other branches in the repository. This allows you to make experimental changes, try out new ideas, or work on different features simultaneously without disrupting the main branch of the code.

Each branch in Git is identified by a name, and the default branch is typically named master. When you create a new branch, you are creating a new pointer to a specific commit, and any new commits made on that branch will be added to that branch pointer and not to the other branches.

Here are the basic steps to create a new branch:
1. Check out the branch you want to base the new branch on: You can create a new branch based on the current branch or any other branch. Use the git checkout command to switch to the branch you want to base the new branch on.
```
git checkout master
```
2. Create the new branch: Use the git branch command to create the new branch. For example, the following command creates a new branch called feature-branch:
```
git branch feature-branch
```
3. Switch to the new branch: Once the new branch is created, use the git checkout command again to switch to the new branch:
```
git checkout feature-branch
```
4. You can merge both 2 & 3 in to one command
```
git checkout -b feature-branch
```
Now you can make changes to the code and commit them on this new branch without affecting the master branch. When the new feature, bugfix or the changes you made are ready, you can merge it back to the main branch, that process is called merging, Git has different ways of merging, such as git merge and git rebase, and it also has ways of resolving conflicts that may arise.

### 15. What is the difference between merge and rebase?
git merge and git rebase are both commands in Git that are used to combine the changes from multiple branches. However, they work in different ways and have different effects on the repository's history.

1. git merge creates a new commit on the current branch that combines the changes from the other branch. This creates a "merge commit" that serves as a marker for the point at which the branches were merged. This is useful for preserving the branch structure in the history and making it clear when certain changes were made.
```
A---B---C---F feature
       \
        D---E master
```
When you use git merge feature on master branch , git will create a new commit G that merges the feature branch into master, keeping the branch structure clear.
```
A---B---C---F feature
       \
        D---E---G master
```
2. git rebase, on the other hand, takes the changes from the other branch and "replays" them on top of the current branch. This effectively "moves" the current branch to the tip of the other branch, and "replays" the commits on top of it. This can be useful for creating a linear history and making it clear which changes were made first. However, it can also cause problems if the other branch has commits that were based on an older version of the current branch.
```
A---B---C--F feature
       \
        D---E---G master
```
When you use git rebase feature on master branch, git will "replay" commits D,E and G on top of commit C and you get a linear history.Here in this case F commit is advanced to C and will be unresolved in history. 
```
A---B---C---F---D'---E'---G master
```
In summary, git merge creates a new merge commit that preserves the branch structure of the repository, while git rebase replays the commits from one branch on top of another, creating a linear history. While git merge is easier to use and understand,git rebase` is generally considered to be a more advanced feature that can be useful for certain use cases such as keeping a linear history and reducing clutter of merge commits. It's important to be aware of what you are doing when using these commands, especially with git rebase, because if the other branch has commits that were based on an older version of the current branch, it can create conflicts that need to be resolved.

### 16. How to delete a branch?
To delete a branch in Git, you can use the git branch -d command followed by the name of the branch you want to delete.
```
git branch -d <branch-name>
```
For example, to delete a branch called feature-branch, you would run:
```
git branch -d feature-branch
```
This command will delete the branch only if it has been fully merged with the branch you are currently on. If the branch you are trying to delete has not been fully merged and contains commits that have not been included in the current branch, Git will prevent the deletion and display an error message. You can force to delete the branch even if it has unmerged commits by using 
```
git branch -D <branch-name>
```
For example:
```
git branch -D feature-branch
```
It's worth noting that when you delete a branch, you're deleting the pointer to a commit, but the commits themselves, and the work you've done on that branch will still exist on other branches or in the repository history. Additionally, if the branch you want to delete is a remote branch, you'll need to use the git push command to delete it. For example, to delete a remote branch called feature-branch on a remote called origin, you would run
```
git push origin --delete feature-branch
```
It's good practice to delete a branch once the work is done, this will help to maintain a clean and organized repository, and avoid confusion about which branches are active and which are not. Also, deleting branches that are no longer needed can help to reduce clutter in the repository and simplify the process of managing branches. When deleting branches, it's important to ensure that you've fully merged the work from the branch you're deleting, and that you have a backup of the work in case you need to access it again in the future. As a final note, when working in a team, it's a good idea to coordinate with other team members before deleting a branch to make sure that no one else is currently working on it. Additionally, if working with remote branches, make sure that others are aware of the deletion to prevent confusion or errors.

### 17. What are the different ways to download the code?

There are several different ways to download the code from a Git repository:
1. Cloning: The most common way to download code from a Git repository is to use the git clone command. This command creates a copy of the entire repository on your local machine, including all of the commits and branches. It also sets up a connection between your local repository and the remote repository, so you can easily stay up-to-date with changes made by other people.
```
git clone https://github.com/user/repo.git
```
2. git pull is a combination of git fetch and git merge commands, it is used to download commits from a remote repository and merge them into the local branch.
```
git pull origin master
```
It will download all new commits from the remote repository and merge them with the current branch you are on. This allows you to easily stay up-to-date with the changes that other people have made.
3. git fetch is similar to git pull, but it only downloads the commits from the remote repository, it does not merge them. This allows you to review the changes before deciding whether or not to merge them into your local branch.
```
git fetch origin master
```
It will download all new commits and create new remote branches that you can use to review the changes and merge them later. This can be useful when you want to review changes before merging them into your local branch.
3. Forking: Another way to download code from a Git repository is to create a "fork" of the repository. This creates a copy of the repository under your own account, which you can then clone to your local machine. This can be useful if you want to make your own changes to the code, and potentially contribute them back to the original repository.

### 18. How to export repository as archive?
The git archive command allows you to export a specific version of the code, either by tag, by commit, or by branch. It creates a tarball of the code, without any of git metadata, it's suitable to distribute the code or share with someone who doesn't have git installed.
```
git archive -o code.zip master
```
Many Git hosting platforms, such as GitHub, allow you to download a zip archive of the code directly from the website. This can be a quick and easy way to get a copy of the code, but it does not include the commit history or the ability to easily stay up-to-date with changes.

### 18. Demonstrate an example of Git Merge with usecase.
1. Create few commits on master
```
  touch f1
  git add .
  git commit -m "a"
  touch f2
  git add .
  git commit -m "b"
```
2. Check the commit history
```
  git log --oneline
```
3. Create a new branch "test" and create few commits on it
```
  git checkout -b test
  touch f3
  git add .
  git commit -m "c"
  touch f4
  git add .
  git commit -m "d"
```
4. Check the commit history
```
  git log --oneline
```
5. Move to master and create few more commits
```
  git checkout master
  touch f5
  git add .
  git commit -m "e"
  touch f6
  git add .
  git commit -m "f"
```
6. Check the commit history
```
  git log --oneline
```
7. Merge test with master
```
  git merge test
```
8. Delete test branch
```
git branch -d test
```
9. Check the commit history
```
  git log --oneline
```

### 19. Demonstrate an example of Git rebase with usecase.
1. Repeat Step1-6 from the above merge scenario
2. To rebase test with master
```
  git checkout test
  git rebase master
  git checkout master
  git merge test
```
3. Check the commit history
```
  git log --oneline
```
### 20. Give me an Usecase for rebase.
Let's say you've created a feature branch called feature-branch based on the master branch. You've been working on this branch for a few days, and in the meantime, other people have been making changes to the master branch.

You want to merge your feature branch back into master, but there are now conflicts because the master branch has moved ahead since you created the feature branch. One way to resolve these conflicts is to merge feature-branch into master, but this would create a merge commit that would make the history of the branch difficult to read, and it also would make it difficult to later on revert the merge.

Instead of merging, you can use git rebase to "replay" your commits on top of the updated master branch. This will take the commits you made on the feature-branch and apply them on top of the master branch, effectively bringing your branch up to date.

### 21. What is git cherry-pick?
git cherry-pick is a command that allows you to selectively apply commits from one branch to another. It can be used to "pick" specific commits and apply them on top of the current branch, instead of merging the entire branch.

For example, imagine you have a branch called feature-branch that has several commits on it. You've made some changes that you want to apply to the master branch, but you don't want to merge the entire branch. Instead, you can use git cherry-pick to apply specific commits from feature-branch to master.

Here's the basic steps of the process:
1. Check out the branch you want to apply the commits to:
```
git checkout master
```
2. Use the git cherry-pick command followed by the commit hash of the changes you want to apply:
```
git cherry-pick <commit-hash>
```
This will apply the specified commit to the master branch. If there are conflicts with the cherry-picked commit, Git will prompt you to resolve them. Once you've resolved the conflicts, you can use git cherry-pick --continue to continue the cherry-pick process. It's worth noting that when you cherry-pick commits, they are not linked to their original branch, the commit will not have the same parent and Git will not be able to track their branch origin. This can make it difficult to revert the changes if needed in the future, it's mostly used when you want to cherry-pick specific commits from a branch that you're not planning to merge it in the near future. It's also useful when you want to fix a specific bug that was fixed in other branch, but you don't want to merge the entire branch or move the entire branch commits to a new branch.

### 22. Demonstrate an example for cherry pick.
1. Create a commit on master
```
  touch f1
  git add .
  git commit -m "a"
```
2. Create a new branch and create few commits on it
```
  git checkout -b test
  touch f2
  git add .
  git commit -m "b"
  touch f3
  git add .
  git commit -m "c"
  touch f4
  git add .
  git commit -m "d"
  touch f5
  git add .
  git commit -m "e"
```
3. To bring only c and d commits to master
```
  git checkout master
  git cherry-pick  c_commiid d_commitid 
```
### 23. What are the types of reset?

git reset is a command that can be used to undo changes in a Git repository. It is a powerful command, and it can be used in several different ways depending on your needs. There are three types of reset in Git:

1. Soft reset: A soft reset, specified with the --soft option, will reset the branch pointer to a specific commit but it will keep the changes in the working tree and the stash. This means that your changes will still be present in the working directory and can be staged or committed again.
```
git reset --soft <commit-hash>
```
Mixed reset: A mixed reset, which is the default if no option is specified, will reset the branch pointer and unstage the changes but will keep the changes in the working tree. This means that the changes will still be present in the working directory, but they will not be staged and can be committed again.
```
git reset <commit-hash>
```
Hard reset: A hard reset, specified with the --hard option, will reset the branch pointer, unstage the changes, and discard any changes in the working tree. This means that any changes that have not been committed will be lost and cannot be recovered.
```
git reset --hard <commit-hash>
```
It's worth noting that when you reset the branch pointer to a commit, it will also delete all commits after the commit you have reseted to, so be careful when using the hard reset option.

git reset is a powerful command and it can be used to undo a wide range of changes in a Git repository, including undoing commits, unmodifying files, and resetting branches to a specific commit

### 24. How we add and delete a remote branch?
When working with Git, it's common to have multiple remote repositories that you interact with. A remote repository is simply a copy of a repository that is hosted on a remote server. You can add and delete branches in remote repositories just as you do on local repositories.

To add a new remote branch, you first need to create a new branch in the local repository, then use the git push command to send the branch to the remote repository.

```
# Create a new branch
git branch new-branch

# Checkout the new branch
git checkout new-branch

# Add some changes to the new branch
echo "new content" >> file.txt
git add file.txt
git commit -m "add new content"

# Push the new branch to remote
git push -u origin new-branch
```

To delete a remote branch, you can use the git push command with the --delete option.
```
git push origin --delete <branch-name>
```
For example, to delete a remote branch called new-branch you would run:
```
git push origin --delete new-branch
```

It's worth noting that git doesn't allow you to delete a branch that you are currently on or delete a branch that you have unmerged commits, you need to switch to another branch or force delete using -D flag, just like when you delete a local branch.
It's also important to be aware that when you delete a branch, you're deleting the pointer to the commits, but the commits themselves and the work you've done on that branch will still exist on other branches or in the repository history.
If you're working in a team, it's a good idea to coordinate with other team members before deleting a branch to make sure that no one else is currently working on it.

### 25. How to recover a deleted branch?
There are a few different ways to recover a deleted branch in Git, depending on the situation. Here are a couple of options:

1. If the branch was recently deleted and you haven't made any new commits since then, you can use the command git reflog to find the branch and check it out again. git reflog shows a log of all the branch updates, so you can find the branch name and then check it out again by using git checkout command.
```
git reflog
f47c5f2 HEAD@{0}: branch: deleted <branch-name>
...
git checkout <branch-name>
```
2. If the branch has been deleted and merged with another branch or the changes have been committed. You can try looking for the branch on the remote repository, you can use the command git branch -a to show remote branches and you should find the deleted branch. Then you can use git fetch to bring the branch down to your local repository, after you can use git checkout to switch to the branch.
```
git branch -a
* master
  remotes/origin/<branch-name>
...
git fetch
git checkout <branch-name>
```
If none of above options works and if you haven't yet made new commits on top of deleted branch, you can try to recover it from a backup or a copy of your repository.
It's worth noting that it is a best practice to regularly push branches you are working on to remote repository and to keep track of merge, deletion or important branch updates, to prevent such kind of issues.

### 26.What is git revert? Give an example.

In Git, revert is a command that undoes the changes made in a commit. It creates a new commit that undoes the changes of a previous one. This is in contrast to reset, which discards commits, discarding changes permanently.

For example, say you have a commit with the SHA hash abc123 that introduced a bug in your code, and you want to undo the changes made in that commit. You would use the command git revert abc123. This would create a new commit that undoes the changes made in the commit with the hash abc123. The commit history would show the original commit and the new revert commit, and the changes made in the original commit would be reversed in the working tree.
```
git revert <commit>
```
It's worth noting that, when you use revert command, the original commit remains in the commit history with all its details, but you will have new commit for the reversion of that commit which undo all the changes done by that commit.

### 27. What is git stash? Give an example.

git stash is a command in Git that allows you to temporarily save changes that you have made to your working directory, but have not yet committed. This allows you to switch branches, or perform other operations on your repository without losing your changes.

For example, imagine you are working on a feature branch and have made some changes to your code, but you need to switch to another branch to fix a bug. Instead of committing your changes and creating a new branch, you can use git stash to save your changes, switch to the other branch, and then apply your changes later using git stash apply.

Here's an example of how you might use git stash:
```
git stash
Saved working directory and index state WIP on feature: abcdefg
HEAD is now at abcdefg 
```
This command saved the state of the current branch on the repository with the name 'WIP' and the commit reference on feature branch. Then you will be able to change to other branch
```
git checkout bugfix
Switched to branch 'bugfix'
```
Once you're done with your work on the bugfix branch and you want to come back to your feature branch and the changes you stashed, you can use
```
git stash apply
```
This command will bring the changes you stashed back to your working directory. When you use the git stash apply command, Git takes the changes that were stashed and applies them to your working directory, but it doesn't switch branches. This means that you will remain on the same branch you were on when you called git stash apply, and the changes you stashed will be added to that branch. git stash apply will bring back the changes in the specific stash you apply, that can be the topmost one you stashed or you can specify which stash you want to apply by its name or id, like git stash apply stash@{2}. It's important to note that when you apply changes from a stash, they are not automatically committed. You will need to use git commit to commit the changes after you've applied them. Additionally, after you've applied the changes from a stash, the stash remains in the repository, allowing you to apply it again in the future if needed. You can also use git stash drop to remove the stash from the repository once you're done with it.

### 28. What is Git tagging? Give an example.
In Git, a tag is a way to mark a specific point in the history of a repository. A tag is a label that you can attach to a specific commit, which allows you to easily refer to that commit in the future. Tagging is commonly used to mark release points in the history of a repository.

There are two types of tags in git: lightweight tags and annotated tags.
1. Lightweight tags are just a simple reference to a specific commit, it's basically a pointer to the commit.
2. Annotated tags are more like a full object in the git database, it contains the tagger name, email, message, and the date it was created in addition to the pointer to the commit.
Here's an example of how you might use tags in Git:
```
git tag -a v1.0 -m "First official release"
```
This command will create an annotated tag called v1.0 on the current commit, the tagger name and email will be taken from git config, and the message will be "First official release".

You can also create lightweight tag by running git tag v1.0 and it will create a tag on the current commit pointing to it, without any extra information.

You can list all the tags by running
```
git tag
```
You can also use the command git show <tag-name> to see the details of a specific tag, like the message and the commit the tag is pointing to. You can push the tags to remote repository using git push --tags or git push origin <tag-name> command, this will allow other developers to pull and access the tag. Tagging is a good practice for marking significant points in the history of a repository, for example releases, milestones, or important bugs fixes, it makes it easier to refer back to specific commits and understand the development history of a project.

### 29. How to change any older commit messages? Give an example.
1. git rebase allows you to modify commits that have already been made, either by changing their commit messages or by squashing multiple commits together.
Here's an example of how you might change the message of an older commit:
```
git rebase -i HEAD~3
```
This command will open an editor where you'll see a list of the last 3 commits in your branch, the oldest commit will be at the bottom. You'll see the word 'pick' before each commit, this is an instruction, this means git will apply this commit. Now you can change the word 'pick' to 'reword' for the commit message you want to change and save the editor.
```
pick abcdefg Initial commit
pick 1234567 Add new feature
reword 9876543 Fix typo in README
```
After you save and close the editor, Git will apply the changes and open another editor for the commit message you've marked 'reword', you can edit the message and save the file again. Once you've done that, Git will update the commit with the new message, and update the SHA-1 hash of the commit, this will cause the child commit of that commit to be affected, so it will change and their hash will change as well.
```
[detached HEAD 3e2e15f] Fix typo in the README
 1 file changed, 1 insertion(+), 1 deletion(-)
```
It's worth noting that you should use this command with caution, as rewriting history can cause problems if other people have already pulled the commits you're modifying. If the commits have been pushed to a remote repository and other people have pulled them, it's best to avoid rewriting them. Instead, you can create new commits that fix the issues in the older commits, and then use git revert to undo the old commits.

2. git commit --amend is another option for changing the message of an older commit. This command allows you to make changes to the latest commit in your branch, by replacing it with a new commit that includes your changes.
When you run git commit --amend, Git opens an editor where you can edit the commit message and make other changes, such as adding or removing files. Once you save and exit the editor, the new commit will be created and the previous commit will be discarded.
This command is useful when you want to make a small modification to the latest commit, such as fixing a typo in the commit message, or adding a forgotten file. However, unlike git rebase, git commit --amend only modifies the latest commit and it doesn't affect other commits in the branch.
Here's an example of how you might use git commit --amend to change the message of the latest commit:
```
git commit --amend -m "Fix typo in commit message"
```
This will create new commit which will replace the previous commit with the new message. This command only updates the last commit and the SHA-1 hash will remain the same, it doesn't affect the other commits or their SHA-1.

That being said, both git rebase -i and git commit --amend allow you to modify the commit message, and the choice between them depends on the specific use case and the status of your branch and repository.

### 30. How to squash multiple commits together in Git?
To squash multiple commits together in Git, you can use the command git rebase -i HEAD~n, where n is the number of commits from the most recent commit that you want to include in the squash. This will open a text editor with a list of the commits and the word "pick" in front of each one. Change the word "pick" to "squash" or "s" for all commits that you want to squash. Save and close the editor, and Git will combine the specified commits into a single commit.

Another way is to use git merge --squash , which will take all the commits and squash them into a single commit, with the added advantage that it keep the branch separate. This command also include a commit message but you will have to provide your own message in this case

Note that squashing commits rewrites the commit history, which can cause problems if the commits have already been pushed to a remote repository that other people are using. So you need to be sure what you are doing before doing so and make sure that other people aren't working on the same branch before you squash.

### 31. What is git pull request? Demonstrate an example without using GithHub.
A pull request is a feature in Git that allows a developer to request that changes they have made on a separate branch be merged into another branch. This is often used in a collaborative development setting, such as when working on an open source project, to allow other developers to review and contribute to the code.

Here is an example of how a pull request might work without using GitHub:
1. Developer A creates a new branch called "feature-x" and makes some changes to the code.
2. Developer A pushes their branch to the central repository.
3. Developer A sends a pull request to the project maintainer, asking that the changes in "feature-x" be merged into the "main" branch.
4. The project maintainer reviews the changes and decides whether to accept the pull request and merge the changes into "main", or to request that the changes be modified in some way before being merged.
5. If the pull request is accepted, the changes are merged into "main" and the "feature-x" branch is deleted or may be kept as per development team agreement.

### 32. How to send pull request using git cli?
Here is an example of how to send a pull request using the Git command line interface:

1. Clone the repository you want to make a pull request to locally.
```
git clone https://github.com/[user]/[repository].git
```
2. Create a new branch for your changes. This branch should be based on the branch you want your changes to be pulled into, usually "main" or "master".
```
git checkout -b [new-branch-name]
```
3. Make your changes and commit them to your new branch.
```
git add [files you want to modify]
git commit -m "Your commit message"
```
4. Push your new branch to the remote repository:
```
git push -u origin [new-branch-name]
```
5. Go to the Git Server Interface and navigate to the repository where you pushed your branch. There you will find an option to create a pull request.
6. Click on "New pull request" button , This will show you a comparison of the changes between your branch and the base branch you want to merge it into.
7. Fill in a title and description for the pull request, and then click the "Create pull request" button.

### 33. What are on prem available Git servers?
There are several on-premises Git servers that you can use to host and manage Git repositories within your own organization, rather than using a cloud-based provider like GitHub or GitLab. Some examples include:
1. Gitea: A self-hosted Git service that is similar in functionality to GitHub and GitLab. It is written in Go and is designed to be lightweight and easy to install.
2. GitBlit: An open-source Git server that runs on a Java servlet container. It has a built-in web interface for managing and browsing Git repositories, and supports several authentication mechanisms.
3. GitBucket: a Git platform powered by Scala with easy installation, high extensibility & GitHub API compatibility.
4. Gerrit: A web-based code review tool for Git-based projects. It is built on top of the JGit library, and provides features for reviewing and approving code changes before they are merged into the main branch.
5. Gogs: similar to Gitea in functionality, Gogs is a lightweight and easy to install Git server written in Go.

### 34. What are market available Git services?
1. GitHub: One of the most widely used Git services, GitHub is a web-based hosting service for Git repositories. It provides a web-based interface for managing and collaborating on Git repositories, as well as a range of tools for code review and collaboration.
2. GitLab: A web-based Git management platform that provides similar functionality to GitHub. It also offers integrated continuous integration and continuous deployment (CI/CD) capabilities, and a built-in issue tracking system.
3. Bitbucket: Git hosting service from Atlassian, it also provides similar functionality to GitHub and GitLab and also provide an integration with their popular Jira project management tool.
4. Azure DevOps: Git hosting service from Microsoft, it also provides similar functionality to above mentioned and it is integrated with Microsoft's cloud-based development tools and services
5. AWS CodeCommit: Git hosting service provided by Amazon Web Services, it is fully managed service that makes it easy to host, manage, and scale Git repositories in the AWS cloud.




