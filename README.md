# Git Branches

## Overview

Continuing on in the Simon Stamp Saga... In this lesson we will learn how to organize sprints of code on different feature branches. This will cover listing, creating, switching, merging, and deleting branches.

## Objectives

1. What are Branches?
2. List Branches
3. Create Branches
4. Change Branches
5. Merge Branches
6. Remove Branches

## Getting to Know Branches

Watch the video below if you are unfamiliar with Git. We will be using Git to access course materials and to share and collaborate on project code throughout this course. After watching the video you may use the text below to review all of the topics discussed in the video.

**Note** that the video uses your computer's terminal, but in this course, you'll be using the Learn IDE and all Git commands will work the same way on it as it does on your terminal.

<iframe width="640" height="480" src="https://www.youtube.com/embed/4sTHVD7rAQA?rel=0" frameborder="0" allowfullscreen></iframe>

### What Are Branches?

Branches are like alternate timelines that we can save our commits to. If you visualize our current branch "master" as the trunk of a tree and all of our commits so far on master are like timestamps along the trunk. If we climb up or down the tree trunk we can fast forward or rewind our code to a particular commit. Now let's say we wanted to build out a new feature in our code, we aren't sure if we will keep the changes or not, so for the sake of flexibility we will create a new branch growing off the trunk of the tree and add commits for our new code feature on that new branch. This way if it turns out that we do not like our code for this feature we can simply cut (delete) that branch off the tree, or if we do like this new feature we can simply merge (combine) that branch back into our trunk (master). 

<!-- The master branch for all intents and purposes is usually left pristine, it is typically the code  we consider to be complete, whole, in a finished state that we would be proud to show the public. If we want to experiment or try out adding a new feature to our code we would typically do that on a different branch. -->

### Listing Branches

In practice it is nice to display a list of all current branches that exist within a repository. In the Learn IDE, cd in to the simon-stamp-collection repo. Now we can type the command `git branch` to display all branches. This returns

```shell
* master
```

Currently since we only have one branch "master" that is all that is listed. The `*` symbol to the left of the branch names shows which branch we are currently working on.

### Create Branches

Let's say we want to create a blog page for our Simon's Stamp Collection project, but we are not sure if we will keep it or not. Whenever we want to build a new feature and have the flexibility to keep it or dispose of it, branches come in handy. Let's create a new feature branch and call it "blog-pages". To do so, type `git checkout -b blog-page` and press return. You might also see people using a shortcut alias fro "checkout" by simply styping "co" instead (the way we do in the video). The "-b" flag states that we are checking out a new branch. This command both creates a new branch and also changes to that branch. the final argument "blog-page" is the name of our branch. It is a convention to use `-` hyphens in branch names, and never to use spaces which will break the command. Now our terminal prompt shows our branch as (blog-page) where it previous had shown (master).

Now let's type that `git branch` command in again and press return. This displays:

```shell
* blog-page
  master
```

This indicates that we now have two branches, "master" and "blog-page". Again the `*` asterisk symbol indicates we are currently working on the "blog-page" branch. Currently, any commits we make will be written on the "blog-page" branch.

Next, let's create a new file. In Terminal type: `touch blog.html` and press return. Then in your code editor open up the blog.html file and paste in the following text:

```txt
Simon's Blog Page
```

Then save the file and head back to Terminal. Type `git add blog.html` and press return, Then type `git commit -m "add blog page"` and press return. Next let's backup this branch's work by pushing it to our remote. Type `git push -u origin blog-page` and press return. This reports:

```shell
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 327 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:jongrover/simon-stamp-collection.git
   * [new branch ]   blog-page -> blog-page
Branch blog-page set uo to track remote branch blog-page from origin.
```

Here we see that the remote recieved our new branch and is tracking changes between our local and remote branch with the same name.

Next, let's go back to the browser and visit our simon-stamp-collection repo on Github. Ohhh, looks like if we click on the centrally located drop menu button that says branches we can see our new remote branch "blog-page" is there.

### Merging Branches

Let's pretend that we have finished up work on our blog page, all the time commiting to our blog-page branch. We have shown the work to Simon and he approves. So we would like to merge our commits from blog-page into our master branch. Back in Terminal we want to first checkout our master branch. Type `git checkout master` and press return. Now we can merge in the changes on our blog-page feature branch by typing `git merge blog-page` and pressing return. This should return something like:

```shell
Updating b41165e..9e719e0
Fast-forward
 blog.html | 1+
 1 file changed, 1 insertion(+)
 create mode 100644 blog.html
```

This shows us that when we merged the commits from the blog-page branch into the master branch, the master branch was updated with 1 new file blog.html. Now let's push our updated master branch back up to our remote. Type `git push origin master` and press return.

Now heading back to Github.com in the simon-stamp-collection repo we can see our master branch now shows the blog.html page in its filelist.

### Deleting Branches

Let's assume we were asked to create a contact page in our Simon's Stamp Collection project. We will start by working on a new feature branch. Type `git checkout -b contact-page` and press return. Then we will make a new file, type `touch contact.html` and press return. Then open the contact.html page in the text editor are of your IDE and paste in the followng text:

```txt
Contact information for Simon.
```

Save this file and jump back to Terminal. Let's stage and commit our changes, type `git add contact.html` and press return, and type `git commit -m "add contact page"` and press return. Then we will push this branch up to our remote. Type `git push -u origin contact-page` and press return.

Let's pretend we finished the contact page and showed it to Simon. Unfortunately Simon doesn't like the page he has decided to get rid of it. This is especially easy because we did all of our commits related to working on the contact page on the contact-page branch. This time instead of merging our branch into master we will instead simply delete the contact page branch.

In order to delete the contact-page barnch we first need to checkout another branch. Type `git checkout master` and press return. Now that we are back on the master branch you can delete the contact-page branch. Type `git branch -d contact-page` and press return. This responds with:

```shell
warning: deleting branch 'contact-page' that has been merged to
         'ref/remotes/origin/contact-page', but not yet merged to HEAD.
Deleted branch contact-page (was 6db62c8).
```

Here Git is letting us know it removed our branch but that it is still existing on our remote origin. Let's type `git branch` and press return to see what branches exist locally.

```shell
  blog-page
* master
```

So locally only the blog-page and master branch exist now and in fact, contact-page has been removed. It does however still exist on our remote origin. In order to also remove the branch from origin type `git push origiin :contact-page` and press return. This should respond with the following:

```shell
To git@github.com:jongrover/simon-stamp-collection.git
 - [deleted]       contact-page
```

This lets us know the contact page was also deleted from the remote. That command again was `git push origiin :contact-page`. The `:` symbol optionally separates the arguments for &lt;local branch&gt;:&lt;remote branch&gt; by leaving the local branch empty and only specifying `:<remote branch>` we are telling the remote to remove that branch.

## Summary

- Branches give us alternate timelines to place commit on.
- This gives us the flexibility to merge and keep or delete and discard the commits on that branch.
- To list branches type `git branch`.
- To create a new branch type `git checkout -b <branch-name>`.
- To switch branches type `git checkout <branch-name>`.
- To merge branches first move to the branch you wish to merge into (e.g. `git checkout master`) and then `git merge <branch-name>`.
- To delete local branches type `git branch -d <branch-name>`.
- To remove branches from a remote type `git push <remote> :<branch-name>`.

## Resources

- [Git Doc - Branch](https://git-scm.com/docs/git-branch)
- [Git Cheatsheet](https://www.git-tower.com/blog/content/posts/54-git-cheat-sheet/git-cheat-sheet-large01.png)
- [Git Best Practices](https://www.git-tower.com/blog/content/posts/54-git-cheat-sheet/git-cheat-sheet-large02.png)
<p class='util--hide'>View <a href='https://learn.co/lessons/html-css-git-branches'>HTML CSS Git Branches </a> on Learn.co and start learning to code for free.</p>
