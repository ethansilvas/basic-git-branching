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

### Making a remote copy of your branch

The new branch you created is only **local** to your computer right now but you can make it public so that you have a remote (backup) copy in case something goes wrong, or just so your team members can see/checkout your new branch. 

Use `git push origin your-branch-name` to create a remote copy of your new branch. The output should look something like: 

![Console output after doing git push to create a remote branch](/images/git-push-branch.png)

In GitHub specifically, you'll notice that if you go to your repository's main page there will be a new popup: 

![Compare and create pull request popup on GitHub repository page](/images/git-new-branch.png)

## Step 5: Aligning your branch with the one you want to merge your changes into

This step is **VERY IMPORTANT** and can also be the hardest one. You need to make sure that your branch has all of the latest changes from `main` or whatever branch you want to merge the changes of your branch into. 



## Step 6: Creating a pull request 

Now that your new branch is done and had been made remote, you're ready to merge your branch's new changes into the main branch. 
