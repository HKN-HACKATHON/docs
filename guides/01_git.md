# **How to use Git**

Git is a version control system that can track changes made on any source file and can be used on any set of computer files, and be useful when coordinating work between different people.  
It is able to create a snapshot of any point on your project, those snapshots are called commits and can be used to save and restore any points of the source history.

### **1\. Setup and Initialization**

To begin using git it should be setted up on your machine, you can find how to install it from [https://git-scm.com/install/](https://git-scm.com/install/).

#### **A. Configure Git Identity**

After the installation, you should configure it by setting up your name and email. This information is used to identify yourself on a commit and is required for their creations.

```shell

git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

#### **B. Initialize a Repository (For New Projects)**

In case you are working on a brand new project, you should tell git to initialize the repository on your project folder

```shell

git init # Initialization of the current project folder
```

### 

#### **C. Start a Project: Cloning an Existing Repository**

If you are working on an already existing project, like the one provided for the Hackathon, you can start working on it by using the clone command, which will download the project repository from the link that you specify.

```shell
git clone https://github.com/user/repository
```

Be aware that source control web sites, such as Github, will require you to authenticate yourself in case you’re trying to clone a private repository. To setup this authentication, you can check at the tutorial on this link [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github) or use the [Github Desktop Application](https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop) on this link [https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/authenticating-to-github-in-github-desktop](https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/authenticating-to-github-in-github-desktop)

### **3\. Staging and Committing Changes**

The creation of a snapshot is managed by the use of the *stage* and *commit* commands, respectively to select a file that will be included in the commit and to create this commit. 

```shell
git add <file-name> # Select a file to add to the commit
git add . # Add the entire folder to the commit
# Create a new commit from the files added
git commit -m "Your descriptive message"

```

Another useful command is the *status* one, which can be used to check which files need to be tracked by git and the ones that were updated.

```shell

git status # Check the files that needs to be updated

```

### **4\. Working with isolated code snapshots**

When working with multiple people on the same repository, it may be necessary to have a personal isolated line of development that is not affected by the changes that they made.  
In git terms, this personal line is called a **branch.** By default, when git initializes a repository it creates a branch called main or master.

To manage branches, the commands that git provides are *branch, checkout* and *switch.*

```shell
# List all of the local branches, add -a to see the remote ones
git branch
# Creates a new branch called <new-branch-name>
git branch <new-branch-name>
# Switch to the local branch <branch-name>
git checkout <branch-name>
# Switch to the local or remote branch <branch-name>
git switch <branch-name>
# Creates and automatically switch to the new branch <new-branch-name>
git checkout -b <new-branch-name>
```

**Pro-Tip:** Always commit or stash your work before switching branches to avoid carrying over unintended changes.

### **5\. Recombine those isolated code snapshots**

After a branch has served its purpose for being created, you may need to recombine (or merge) it with another branch to restore the initial development flow disrupted by this isolation and update the other branches.

```shell
# Combine all the updates of the branch <branch-name> with the currently selected one
git merge <branch-name>
```

Be aware that you may have conflicting changes on one or more files, in this case git will require you to manually solve them by selecting the correct change that needs to be present in the branch that you are updating.

### **6\. Saving and getting changes from a Remote Repositories**

One of the features of git that make it possible to collaborate with other people, is the ability to use remote repositories to send and receive source code updates.  
The git way of working with such repositories is done with the commands *push* and *pull*, which respectively send and receive changes from the remote repository.

```shell
# Send your changes on branch <branch-name> to the remote called origin and set it as the default
git push -u origin <branch-name>
# Send your changes to the default remote on your current branch
git push
# Get the changes on branch <branch-name> from the remote origin
git pull origin <branch-name>

# Get the changes from the default remote on your current branch
git pull
```

## **Note:** After you push changes on a different branch than the default one, you may use Github to merge those changes by using the pull request feature. This can be helpful in case you want to explain and discuss your changes and if you do not want to use the command line to manage merges.
