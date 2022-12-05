# My basic guide to using git branches to share with my friends :D 

## Quick and simple steps (more details of each step is provided in their corresponding sections)

[Step 1](#step-1-make-sure-you-are-in-the-branch-that-you-want-to-base-your-new-branch-off-of): Checkout the main branch with `git checkout main`. Update your main branch with `git pull`. <br>

[Step 2](#step-2-create-your-new-branch): Create your new branch with `git checkout -b your-branch-name` <br>

[Step 3 or 4](#step-3-or-4-code-what-you-need-and-keep-your-branch-up-to-date): Code whatever you need to do, but remember that you'll need to keep your branch up to date with main. Whenever you're at a good stopping point while you're coding, and you know that there are new changes in main, update your branch with the latest version of main by doing:

1. Commit any changes you have in your branch (you can't have uncommitted changes when rebasing)

    IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first): Make sure the remote version of your branch has the latest committed changes with `git push origin your-branch-name`

2. Checkout main with `git checkout main`
3. Update your main with `git pull`
4. Go back to your branch with `git checkout your-branch-name`
5. Update your branch with the latest version of main with `git rebase main`

    IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first): Now that your branch has been rebased with main, you'll have to update the remote version of your branch to reflect that by doing another `git push origin your-branch-name`

Steps to deal with merge conflicts are listed in the [Fixing a merge conflict](#fixing-a-merge-conflict) section. <br>
Steps to deal with merge conflicts for Jupyter notebooks are in the [Fixing merge conflicts in a jupyter notebook](#fixing-merge-conflicts-in-a-jupyter-notebook) section.

[Step 4 or 3](#step-4-or-3-making-a-remote-copy-of-your-branch): Make a remote copy of your branch by doing `git push origin your-branch-name`. You can verify that it worked on your repository's GitHub page, under the "branches" section. <br>

[Step 5](#step-5-creating-a-pull-request): Go to your repository's GitHub page (or GitHub Desktop), find your branch, click the "New pull request", write a descriptive title and description of your changes in the provided boxes, and then click "Create pull request". After that, you're all done and someone will likely review your changes. 

If the reviewer finds a bug or something to change you can go back and fix it in your code, commit your changes, and update your remote branch with `git push origin your-branch-name`. The pull request will automatically know that you've updated the branch  <br><br>

**Should I do step 3 or 4 first?** - If you want to make a remote/backup copy of your branch, then do step 4 before step 3. You don't technically need to make a remote copy of your branch until you are done coding and ready to push your new branch's code to the main branch, but without a remote copy you won't have a backup of your branch in case of disaster! <br><br>

---

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

The main purpose of branching is to basically make a copy of a branch, `main` for example, for you to implement your new feature without worrying about messing up all the good code in the original branch. You are now ready to code in your new branch!

### Keeping your branch up to date 

This is **VERY IMPORTANT** and can also be the very difficult. You need to make sure that your branch is up to date with `main` or whatever branch you want to merge the changes of your branch into. 

Ideally, all you need to do is the steps that were listed above:
1. Commit any changes you have in your branch (you can't have uncommitted changes when rebasing)

    IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first): Make sure the remote version of your branch has the latest committed changes with `git push origin your-branch-name`

2. Checkout main with `git checkout main`
3. Update your main with `git pull`
4. Go back to your branch with `git checkout your-branch-name`
5. Update your branch with the latest version of main with `git rebase main`

    IF YOUR BRANCH HAS A REMOTE VERSION (you did step 4 first): Now that your branch has been rebased with main, you'll have to update the remote version of your branch to reflect that by doing another `git push origin your-branch-name`

Unfortunately, doing this will sometimes result in a **merge conflict** which can be very difficult to fix. VSCode or your terminal will scream at you if this happens and if so you can do the following optional steps:

### Fixing a merge conflict

1. If this is your first time dealing with merge conflicts, you probably haven't set VSCode (or your preferred text editor) to be your git editor. If you haven't, then it is likely that your console appears to be running/stuck because of the failed rebase. You can stop this by either doing Control+c on your keyboard, or by typing `q` and pressing enter in the console. If you have set VSCode to be your editor and your console appears to be normal, then you're safe to move on. 

2. Now that your console is back to normal, you can revert back to as if you never tried to rebase by doing `git rebase --abort`. 

3. Make sure that VSCode (or preferred text editor) is your git editor by doing `git config --global core.editor "code --wait"`. 

4. With VSCode as your editor, retry the rebase with `git rebase main`. 

5. In your "Source Control" tab on the left bar, you will notice that there will be a list of files that have conflicts. You can tell that they have conflicts by opening them and looking for big blocks that look like: 

![Current/incoming changes in a VSCode window to resolve merge conflicts](/images/vscode-merge-conflict.png) <br>

6. Each of these cases that VSCode is marking with "Current Change" and "Incoming Change" are places where Git can't decide which change it should make. These issues usually happen when people make different changes to the same line in the file. Go through each of these and use your best judgement to decide which lines of code should remain.

7. Save the file once you are done with all the highlighted conflicts 

8. Open the Source Control tab in VSCode, all of the conflicting files will show up almost like when you're making a normal commit. Make sure to stage all of the files by hovering over the "+" button

![Plus sign button on VSCode committed file for staging](/images/vscode-stage-button.png)

9. Press the commit button to finish this part of the rebase. You can optionally change the commit message but it's better to just keep the original one that it has in there. 

10. Keep doing steps 6-9 until the rebase is done. VSCode is pretty good at automatically doing this but if it doesn't seem like it's doing anything try doing `git rebase --continue`. 

### Fixing merge conflicts in a Jupyter notebook

Git tracks changes in Jupyter notebooks in their raw format which is a giant JSON file that makes it basically impossible to resolve merge conflicts the normal way. There are a few ways to solve this but I have found [nbdime](https://nbdime.readthedocs.io/en/latest/) to be incredibly easy to use for what I need it for. 

The following steps are similar to the section above (for solving normal merge conflicts), but I have repeated some steps in case this is your first time dealing with merge conflicts:

1. If this is your first time dealing with merge conflicts, you probably haven't set VSCode (or your preferred text editor) to be your git editor. If you haven't, then it is likely that your console appears to be running/stuck because of the failed rebase. You can stop this by either doing Control+c on your keyboard, or by typing `q` and pressing enter in the console. If you have set VSCode to be your editor and your console appears to be normal, then you're safe to move on. 

2. Now that your console is back to normal, you can revert back to as if you never tried to rebase by doing `git rebase --abort`. 

3. Make sure that VSCode (or preferred text editor) is your git editor by doing `git config --global core.editor "code --wait"`. 

4. With VSCode as your editor, retry the rebase with `git rebase main`.

5. Here, you can see what I was mentioning at the start of this section. You can view the files that have merge conflicts in the "Source Control" tab on the left bar of VSCode. However, when you open them to see the conflicts you will see how impossible it is to try to resolve them this way (the normal way). This is what nbdime is for: 

(You can start at step 6 if you have VSCode set to your git editor and have done `git rebase --abort` to reset back to before your rebase failed)<br>

6. Make sure that your dev environment is turned on. You're likely using a conda dev environment which would be `conda activate your-env-name`. 

7. Do `pip install nbdime`.

8. Verify that it worked by doing `conda list nbdime`. 

9. I only need nbdime for resolving merge conflicts, and for that you can just do `git-nbmergetool config --enable`. If you want the other features, you would do `nbdime config-git --enable`. 

    **YOU WILL HAVE TO DO THIS STEP ONCE FOR EVERY REPOSITORY**

    If you want to understand more about what this is doing, go into your repository in your system's file manager, show the hidden files, and go into your .git folder to open the 'config' file in it. If you haven't messed around with this repository's git config file before, you'll see all the changes made after the [branch "main"] section. 

10. Now you can retry your rebase by doing `git rebase main`. 

    **NOTE:** For very large notebooks with lots of outputs, doing the rebase will take a LONG time. You will know this is the case when your console looks like it's stuck/loading and if in your files you'll see a bunch of newly created files that have weird names like "MERGE&FILE" or something like that. 
    
    This should be fine and will hopefully take a few minutes depending on the size of your file. You will know when it's done when your console is back to normal and you'll see in the "Source Control" tab that your files look like how they normally would when using VSCode to resolve merge conflicts.

11. Open the nbdime merge editor by doing `git mergetool --tool=nbdime your-notebook-name.ipynb`

12. The editor will open in your browser and look something like: 

![Header of nbd editor in browser that shows Notebook Merge and other items](/images/nbd-editor.png)

13. Now you can scroll through your whole notebook cell-by-cell. Although it's a lot to take in, just know that there isn't actually a whole lot for you to do at this point!

14. First, 

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
