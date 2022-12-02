# My basic guide to using git branches to share with my friends :D 

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

## Step 3: Code

The main purpose of branching is to basically make a copy of a branch, `main` for example, for you to implement your new feature without worrying about messing up all your good code in the original branch. You are now ready to code in your new branch!

## Step 4: Making a remote copy of your branch

**NOTE:** You don't technically need to make a remote copy of your branch until you are done coding and ready to push your new branch's code to the main branch, but without a remote copy you won't have a backup of your branch in case of disaster!

The new branch you created is only **local** to your computer right now but you can make it public so that you have a remote (backup) copy in case something goes wrong, or just so your team members can see/checkout your new branch. 

Use `git push origin your-branch-name` to create a remote copy of your new branch. The output should look something like: 

![Console output after doing git push to create a remote branch](/images/git-push-branch.png)

In GitHub specifically, you'll notice that if you go to your repository's main page there will be a new popup: 

![Compare and create pull request popup on GitHub repository page](/images/git-new-branch.png)

## Step 5: Aligning your branch with the one you want to merge your changes into

This step is **VERY IMPORTANT** and can also be the hardest one. You need to make sure that your branch has all of the latest changes from `main` or whatever branch you want to merge the changes of your branch into. 

Ideally, all you need to do is `git pull origin main --rebase` or just `git pull origin main` (rebase is better in my opinion since it just puts all of your branch's commits after the latest ones in main, rather than mixing them in between based on when the commits were made).

Unfortunately, doing this pull will sometimes result in a **merge conflict** which can be very difficult to fix. VSCode or your terminal will scream at you if this happens and if so you can do the following optional steps:

### Fixing a merge conflict

If VSCode is screaming at you and you tried to rebase but it's stuck and everything is a disaster, don't worry this is normal! 

1. If the rebase failed and you are stuck you can do `git rebase --abort`. 
2. You will want to set VSCode to be your git editor by doing `git config --global core.editor "code --wait"`
3. With VSCode as your editor, retry the rebase with `git pull origin main --rebase`
4. Now VSCode will go through each of the commits that make a merge conflict and will open the corresponding files with edits that look like: 

![Current/incoming changes in a VSCode window to resolve merge conflicts](/images/vscode-merge-conflict.png) <br>

5. Each of these cases that VSCode is marking with "Current Change" and "Incoming Change" are places where Git can't decide which change it should make. These issues usually happen when people make different changes to the same line in the file. Go through each of these and use your best judgement to decide which lines of code should remain.
6. Save the file once you are done with all the highlighted conflicts 
7. Open the Source Control tab in VSCode, all of the conflicting files will show up almost like when you're making a normal commit. Make sure to stage all of the files by hovering over the "+" button

![Plus sign button on VSCode committed file for staging](/images/vscode-stage-button.png)

8. Press the commit button to finish this part of the rebase. You can optionally change the commit message but it's better to just keep the original one that it has in there. 
9. Keep doing steps 5-8 until the rebase is done. VSCode is pretty good at automatically doing this but if it doesn't seem like it's doing anything try doing `git rebase --continue`. 


## Step 6: Creating a pull request 

Now that your new branch is done, it has been made remote, and it's been updated with main's most recent changes, you're ready to merge your branch's new changes into the main branch. 

Go to your repository's main page (or GitHub desktop) and find your branch. If you just pushed your branch then there might be a big popup that will take you to it, otherwise you can click "branches":

![Branches button next to main branch name in GitHub repository main page](/images/git-branches.png)

Find your branch and click "New pull request". This will take you to a page that should say something like "Able to merge" and lets you provide a title and description of what your changes were: 

![Creating a pull request in GitHub with description text box](/images/git-create-pr.png)

You can also verify that all your changes are as they should be by scrolling down and looking at the individual files that were changed: 

![GitHub list of files and places in the files that were changed in the branch](/images/git-pr-changes.png)

Press the "Create Pull Request" button and your pull request will be ready to be reviewed by your team! 

Usually the project lead or whoever approves your pull request will actually merge it, but in case you need to do it there will likely be a big "Merge Changes" button once it gets approved. 
