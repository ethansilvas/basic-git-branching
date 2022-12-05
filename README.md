# My basic guide to using git branches to share with my friends :D 

## Quick and simple steps (context of each step is provided in the corresponding sections after this one)

[Step 1](#step-1-make-sure-you-are-in-the-branch-that-you-want-to-base-your-new-branch-off-of): Checkout the main branch with `git checkout main`. Update your main branch with `git pull`. <br>

[Step 2](#step-2-create-your-new-branch): Create your new branch with `git checkout -b your-branch-name` <br>

[Step 3 or 4](#step-3-or-4-code-what-you-need-and-keep-your-branch-up-to-date): Code whatever you need to do, but remember that you'll need to keep your branch up to date with main. Whenever you're at a good stopping point while you're coding, and you know that there are new changes in main, update your branch with the latest version of main by doing:

1. Commit any changes you have in your branch (you can't have uncommitted changes when rebasing)

IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first) DO THIS, IF NOT THEN SKIP: Make sure the remote version of your branch has the latest committed changes with `git push origin your-branch-name`

2. Checkout main with `git checkout main`
3. Update your main with `git pull`
4. Go back to your branch with `git checkout your-branch-name`
5. Update your branch with the latest version of main with `git rebase main`

IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first) DO THIS, IF NOT THEN SKIP: Now that your branch has been rebased with main, you'll have to update the remote version of your branch to reflect that by doing another `git push origin your-branch-name`


Steps to deal with merge conflicts are listed in the [Fixing a merge conflict](#fixing-a-merge-conflict) section. 

[Step 4 or 3](#step-4-or-3-making-a-remote-copy-of-your-branch): Make a remote copy of your branch by doing `git push origin your-branch-name`. You can verify that it worked on your repository's GitHub page, under the "branches" section. <br>

[Step 5](#step-5-creating-a-pull-request): Go to your repository's GitHub page (or GitHub Desktop), find your branch, click the "New pull request", write a descriptive title and description of your changes in the provided boxes, and then click "Create pull request". After that, you're all done and someone will likely review your changes. 

If the reviewer finds a bug or something to change you can go back and fix it in your code, commit your changes, and update your remote branch with `git push origin your-branch-name`. The pull request will automatically know that you've updated the branch  <br><br>

**NOTE:** If you want to make a remove/backup copy of your branch, then do step 4 before step 3. You don't technically need to make a remote copy of your branch until you are done coding and ready to push your new branch's code to the main branch, but without a remote copy you won't have a backup of your branch in case of disaster!

## Step 1: Make sure you are in the branch that you want to base your NEW branch off of

Most likely you want to make your new branch off of `main`. Make sure you have no active changes in your code and switch to this branch by doing `git checkout main` in your console. 

You can tell if you have "active changes" by looking at the Source Control button on the left sidebar of VSCode. The button will have a number on it if you have changes, but to be safe you usually don't want to switch branches with active changes. <br>
![VSCode Source Control button with two active changes](/images/vscode-active-changes.png)

Remember, you are checking out your **local** version of main, not the remote version. This means that you will need to make sure to **pull** from the remote main to update your local main.

You can pull to update your main a few different ways: 
1. Do `git pull` in the command line
2. Press the refresh button next to the branch name in VSCode (bottom left of window)<br>
![Push and pull button in the bottom left of VSCode](/images/vscode-refresh.png)
3. There is probably something similar to step 2 in GitHub Desktop

After pulling it should either print out all the new commits that you were missing or it will just print out "Already up to date."

## Step 2: Create your new branch

Think of a descriptive branch name based on the task that you're working on use the checkout command to create a new branch with this name. 

The basic structure of the checkout command is `git checkout -b your-branch-name`.

If I wanted to make a branch called `fixed-readme-typos` then I would do `git checkout -b fixed-readme-typos`.

There are other ways to create a branch and then check it out, but this command does it all in one. If all goes well then you will notice in the bottom left corver of VSCode that instead of saying `main` it will have switched to your new branch name. 

## Step 3 or 4: Code what you need and keep your branch up to date

The main purpose of branching is to basically make a copy of a branch, `main` for example, for you to implement your new feature without worrying about messing up all your good code in the original branch. You are now ready to code in your new branch!

### Keeping your branch up to date 

This step is **VERY IMPORTANT** and can also be the hardest one. You need to make sure that your branch is up to date with `main` or whatever branch you want to merge the changes of your branch into. 

Ideally, all you need to do is the steps that were listed above:
1. Commit any changes you have in your branch (you can't have uncommitted changes when rebasing)

IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first) DO THIS, IF NOT THEN SKIP: Make sure the remote version of your branch has the latest committed changes with `git push origin your-branch-name`

2. Checkout main with `git checkout main`
3. Update your main with `git pull`
4. Go back to your branch with `git checkout your-branch-name`
5. Update your branch with the latest version of main with `git rebase main`

IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first) DO THIS, IF NOT THEN SKIP: Now that your branch has been rebased with main, you'll have to update the remote version of your branch to reflect that by doing another `git push origin your-branch-name`

Unfortunately, doing this will sometimes result in a **merge conflict** which can be very difficult to fix. VSCode or your terminal will scream at you if this happens and if so you can do the following optional steps:

### Fixing a merge conflict

If VSCode is screaming at you and you tried to rebase but it's stuck and everything is a disaster, don't worry this is normal! 

1. If the rebase failed and you are stuck you can do `git rebase --abort`. 
2. You will want to set VSCode to be your git editor by doing `git config --global core.editor "code --wait"`
3. With VSCode as your editor, retry the rebase with `git rebase main`
4. Now VSCode will go through each of the commits that make a merge conflict and will open the corresponding files with edits that look like: 

![Current/incoming changes in a VSCode window to resolve merge conflicts](/images/vscode-merge-conflict.png) <br>

5. Each of these cases that VSCode is marking with "Current Change" and "Incoming Change" are places where Git can't decide which change it should make. These issues usually happen when people make different changes to the same line in the file. Go through each of these and use your best judgement to decide which lines of code should remain.
6. Save the file once you are done with all the highlighted conflicts 
7. Open the Source Control tab in VSCode, all of the conflicting files will show up almost like when you're making a normal commit. Make sure to stage all of the files by hovering over the "+" button

![Plus sign button on VSCode committed file for staging](/images/vscode-stage-button.png)

8. Press the commit button to finish this part of the rebase. You can optionally change the commit message but it's better to just keep the original one that it has in there. 
9. Keep doing steps 5-8 until the rebase is done. VSCode is pretty good at automatically doing this but if it doesn't seem like it's doing anything try doing `git rebase --continue`. 

## Step 4 or 3: Making a remote copy of your branch

The new branch you created is only **local** to your computer right now but you can make it public so that you have a remote (backup) copy in case something goes wrong, or just so your team members can see/checkout your new branch. 

Use `git push origin your-branch-name` to create a remote copy of your branch. The output should look something like: 

![Console output after doing git push to create a remote branch](/images/git-push-branch.png)

In GitHub specifically, you'll notice that if you go to your repository's main page there will be a new popup: 

![Compare and create pull request popup on GitHub repository page](/images/git-new-branch.png)

## Step 5: Creating a pull request 

Now that your new branch is done, it has been made remote, and it's been updated with main's most recent changes, you're ready to merge your branch's new changes into the main branch. 

Go to your repository's main page (or GitHub desktop) and find your branch. If you just pushed your branch then there might be a big popup that will take you to it, otherwise you can click "branches":

![Branches button next to main branch name in GitHub repository main page](/images/git-branches.png)

Find your branch and click "New pull request". This will take you to a page that should say something like "Able to merge" and lets you provide a title and description of what your changes were: 

![Creating a pull request in GitHub with description text box](/images/git-create-pr.png)

You can also verify that all your changes are as they should be by scrolling down and looking at the individual files that were changed: 

![GitHub list of files and places in the files that were changed in the branch](/images/git-pr-changes.png)

Press the "Create Pull Request" button and your pull request will be ready to be reviewed by your team! 

Usually the project lead or whoever approves your pull request will actually merge it, but in case you need to do it there will likely be a big "Merge Changes" button once it gets approved. 
