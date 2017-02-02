#Git basic commands

##Create repos

In your app folder, initialize your git repos with :

```
git init
```

##Clone repos

To create a local copy of your repos :

```
git clone /path/to/repository
```

To get a remote repos (on github, bitbucket, gitlab, git server...) :

```
git clone username@host:/path/to/repository
```

##Tree

Your local repos is composed of 3 "trees" generated by git
* The first is your workspace which contains your files
* The second is an Index which is a transit area for your files
* Finally the **Head** which pointing on the last commit

Working dir --- add ---> index (stage) --- commit --> HEAD

##Add and validate

To add a file to the index, use 

```
git add <file name>

or 

git add *
```

It is the first step in the basic git workflow. Then to validate some updates :

```
git commit -m "your commit message. be explicit"
```

It will add your file to the **Head** but the file si not yet in your remote repos

##Sending updates

Now you have to send your **Head** in your remote repos

```
git push origin <branch name>

git push origin master
```

If you have not cloned your existing repos and would to connect it with your remote repos, you have to add it before :

```
git remote add origin
```

##Branches

Branches allows you to work on specific features without impact the rest of your project

By default, the **master** branch is created by the init. Then you you can create all the branches you want, but don't forget to merge them with the master when you have finished.

###Create branch

```
git checkout -b <branch name>
```

###Back to master

```
git checkout master
```

###Delete branch

```
git branch -d <branch name>
```

> A new branch is not visible for other users as long as you have not push it on origin

```
git push origin
```

##Update and Merge

###Update local repos

```
git pull
```

###Merge branches

If you want to merge your **dev** branch to your **master**, first switch to target branch (here **master**) and do a merge with the branch to merge

```
git checkout master
git merge dev
```

###Merge conflicts
Git will automatically merge updates. But sometimes there are some merge conflicts to resolve manually.

After you have resolve all conflicts, you have to add them
```
git add
```

To get an overview of updates
```
git diff
```

##Tags

It is recommanded to create tag to identify your releases. To create a tag, you have to get the first 10 characters of your last commit id (you can use other string as id but the id must be unique)

```
git tag 1.0.0 1b2e1d63ff
```

Use ```git log```to get your commit list

##Replace local updates

In case of you have make a mistake in your work tree, you can cancel your local updates with :

```
git checkout -
```

This will replace the updates in your work tree with the last **Head** content. Note that all added (wrong) updates will be kept by the index.

If you want delete all updates and local values, get the last history from the remote server and point to the main local branch on it like


```
git fetch origin
git reset -hard origin/master
```