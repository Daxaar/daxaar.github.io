---
layout: post
title: Digging into remote branches in git
excerpt: 
author: daxaar
categories:
  - GIT

tags:

draft: false
---
This post assumes a basic understanding of git and the principles of commits, branches and remote repositories. I wrote up this post after playing around with remotes beyond just configuring remote tracking branches for some unrelated work.

It looks at how a remote tracking branch is setup and might be useful to people confused by what a remote tracking branch really is. It also helps clear up some of the confusion regarding how git "connects" your local and remote repositories.

As this post is based off some notes I was taking for some unrelated work it only covers the porcelain, it doesn't dig into anything regarding the reflog.

So what are we going to be doing?

<ol>
<li>Creating a couple of local repositories. One of them will be our remote but it'll all be configured using local folders.</li>
<li>Setting up one of the repositories to use the other as a remote.</li>
<li>Setting up a remote tracking branch for master.</li>
<li>Seeing how we can actually have a local feature branch configured to pull from the same remote branch as our master. This demonstrates that there isn't a 1-1 relationship between master on your local machine and master on the remote server.  And what is master anyway?</li>
<li>Changing the remote tracking branch for the local feature branch.</li>
</ol>

You can follow along by simply reading the explanatory text and executing the command given immediately beneath.  In some circumstances I've included the output from the terminal as a result of executing the command for further discussion.  These commands assume your working in a *nix environment but if you're on Windows you can adjust the paths accordingly.  Better still, just fire up git bash which would have most likely been installed as part of your git install.  For terminal (command line) work bash is so far ahead of cmd and powershell.

First let's setup our folder structure.  The following command(s) will create the required folder structure under your home directory and navigate into it.

~~~ bash
mkdir ~/remotes-tutorial && cd ~/remotes-tutorial
mkdir r1 && mkdir r2

~~~

Create a new git repo in the r1 folder you're now in

~~~
git init --bare
~~~

Check the manpage for details on the `--bare` option.

Change to the r2 directory

~~~
cd && cd r2
~~~

Initialise another git repo here (notice we don't use `--bare`).

~~~
git init
~~~

You'll see that we have no remotes configured.

~~~
git remote
~~~

Configure this repo to use r1 as a remote

~~~
git remote add origin ~/remotes-tutorial/r1
~~~


Let's check what this has done

~~~
git remote show origin
~~~

The output in the terminal will show we now have the r1 repository configured as a remote, but HEAD branch: (unknown) shows we have no tracking branches yet. That is, none of our local branches have been based off of a remote commit. This is a significant part of understanding tracking branches. A branch does not exist in git in the same way as it does in Mercurial, SVN or TFS etc. A branch is merely a named commit.

When you "connect" your local branch to a remote branch you are merely basing your local branch (the next commit) off of a commit on the remote branch which is reflected in your local repository as the tracking branch. It is from this branch that you base your local branch.

When you see those messages in the terminal showing the number of commits you are ahead or behind the remote, git is merely counting the number of commits on your local branch since you merged with the local tracking branch. This number will change when you do a git fetch as you are now updating the tracking branch to reflect any changes made to the remote branch. A pull is different in that it will do is a fetch to the local tracking branch and immediately try and merge to your local branch.

OK, this is going off on a tangent. Let's get back to where we were.

So we have our remote setup but no tracking branches. That is to say our local master isn't tracking the remote master. Let's set that up now by pushing our local master branch to the remote.

~~~
git push origin master
~~~

An error!
~~~
error: src refspec master does not match any
~~~

Don't panic, any errors we see along the way are intentional. What this means is that git doesn't know what master is. Remember <strong>a branch is just a named commit</strong> and we haven't made any commits to our repo yet so somewhat unsurprisingly master doesn't exist. Let's prove this.

~~~
git branch
~~~

You should see nothing coming back in the terminal because we don't have any branches yet or more specifically we don't have any commits.

Let's make a quick commit.

~~~ bash
touch file
git add .
git commit -m &#039;initial commit&#039;
~~~

Now lets see what branches we have

~~~
git branch
~~~

OK, we now have master. But why master? This name is simply the default name given to the branch when the first commit is made. If we'd wanted to we could have created a branch called wibble before making the first commit and master would never exist!

OK, so now let's get back to pushing our master branch to the remote.

~~~
git push origin master
~~~

Now let's see what our remote looks like in relation to our master branch

~~~
git remote show origin
~~~


~~~ bash
Fetch URL: /Users/darren/remotes-tutorial/r1
Push URL: /Users/darren/remotes-tutorial/r1
HEAD branch: master
Remote branch:
master tracked
Local ref configured for git push:
master pushes to master (up to date)
~~~
The key thing here is that our master is now tracking master in the remote repo. If we wanted to we could checkout the remote tracking branch. But remember, we're checking out our local copy of the remote (The D in DVCS) and again, this is just a named commit in the repository. No changes we make here will affect the actual remote repository.

~~~
git checkout origin/master
~~~

~~~
You are in detached HEAD state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

git checkout -b

HEAD is now at e764596... initial commit
~~~

Detached HEAD? Sounds painful. The warning message is quite self explanatory but essentially from this we can see that we cannot make any changes to this branch but we can create a new branch using this as our starting point. A branch (and that includes the remote tracking branch origin/master) is simply a commit within the repository.

Let's go off piste a little here now. Remember, our local master is already tracking origin/master but we can still base a new branch off this branch because it's just another commit in the repository.

Let's assume we want to make some changes...

~~~
git checkout origin/master -b new_feature
~~~

~~~
Branch new_feature set up to track remote branch master from origin.
Switched to a new branch &#039;new_feature&#039;
~~~

This creates a new branch called `new_feature` which has been setup automatically to track origin/master. Let's look at how our remote is now configured

~~~
git remote show origin
~~~

~~~
Fetch URL: /Users/darren/remotes-tutorial/r1
Push URL: /Users/darren/remotes-tutorial/r1
HEAD branch: master
Remote branch:
master tracked
Local branch configured for &#039;git pull&#039;:
new_feature merges with remote master
Local ref configured for &#039;git push&#039;:
master pushes to master (up to date)
~~~

As you can see our new_feature branch is tracking origin/master when we pull but significantly it isn't configured to allow us to push to origin/master. Only one local branch (ref in the message above) can be configured to push which makes sense.

This now means that whenever we do a `git pull origin master` it will be merged automatically into <strong>both</strong> the master and new_feature branches. Typically this isn't something you'd want to do, especially on master. However, this shows there isn't a linear one to one relationship between a remote branch and a local branch. As I've eluded to a few times in this post already, a branch is nothing more than a named commit within the repository.

Let's make a change on new_feature and push to the remote to see what happens. Remember, we have to make the commit because, repeat after me..."A branch is just a named commit" and without any commits on new_feature it doesn't really exist (other than in the reflog but we'll cover that little gem in another post).

~~~ bash
touch fileonnew_feature
git add .
git commit -m "added new file"
~~~

~~~
git push origin new_feature
~~~

~~~
Fetch URL: /Users/darren/remotes-tutorial/r1
Push URL: /Users/darren/remotes-tutorial/r1
HEAD branch: master
Remote branches:
master tracked
new_feature tracked
Local branch configured for &#039;git pull&#039;:
new_feature merges with remote master
Local refs configured for &#039;git push&#039;:
master pushes to master (up to date)
new_feature pushes to new_feature (up to date)
~~~

OK we can see that new_feature now exists in the remote and we're tracking it. However, notice that new_feature is configured to merge from remote master when we do a git pull. This is because if you remember we based new_feature off of origin/master. Although there is nothing wrong with doing this it's not what we want so let's see how we can change this behaviour so new_feature tracks changes to remote new_feature when we pull.

~~~
git branch new_feature --set-upstream-to origin/new_feature
~~~

Ok now let's look at how our remotes are setup

~~~
git remote show origin
~~~

~~~
* remote origin
Fetch URL: /Users/darren/remotes-tutorial/r1
Push URL: /Users/darren/remotes-tutorial/r1
HEAD branch: master
Remote branches:
master tracked
new_feature tracked
Local branch configured for &#039;git pull&#039;:
new_feature merges with remote new_feature
Local refs configured for &#039;git push&#039;:
master pushes to master (up to date)
new_feature pushes to new_feature (up to date)
~~~

Excellent, we have new_feature tracking origin/new_feature for push and pull.

If there is one thing you should take away from this post it's that branches are just named commits. I hope this post has helped you understand a little more about how remote tracking branches work and their relationship to local branches.

Did I mention, "branches are just named commits"? :-)

Have fun!
