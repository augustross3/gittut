# Git Tutorial

Welcome to this detailed Git tutorial. Through this guide, you'll learn how to use Git from the command line by applying the commands in the context of a small coding project. The goal is for you to be comfortable using Git for version control in your own projects, covering the basics of initializing repositories, making commits, understanding branches, and using merging.

## Getting Started with Git

Before diving into Git commands, ensure Git is installed on your computer. Open a terminal and type the following command to check if Git is installed:

```
git --version
```

If Git is not installed, follow the installation instructions available on the official Git website.

[Official Git Website](https://git-scm.com/downloads)

### Setting Up Your First Repository

1. **Create a directory for your project**: This is where your project files will live on your computer. Use the `mkdir` command followed by your project's name, then navigate into your newly created directory with `cd`.

```
mkdir my_git_project
```

```
cd my_git_project
```

2. **Initialize a new Git repository**: Inside your project directory, use `git init` to initialize a new Git repository. This command creates a hidden `.git` directory, which Git uses to track changes.

```
git init
```

### Making Your First Commit

(Note: From this point on, the tutorial assumes you have Python installed. However, feel free to translate this tutorial to the language of your choice, just make sure to switch out file extensions in the commands and to write the proper syntax for your language in any echo calls)

1. **Create a Python script**: Start by creating a simple script named `hello_git.py` that prints a message. This will be the first file in your Git repository.

    ```
    echo "print('Hello, Git!')" > hello_git.py
    ```

2. **Add the file to the staging area**: Before committing any changes, you need to add them to the staging area with `git add`. This step prepares changes for a commit.

    ```
    git add hello_git.py
    ```

    Alternatively, you can use `git stage` which is synonymous with `git add` and serves the same purpose of adding changes to the staging area. 

    ```
    git stage hello_git.py
    ```

3. **Commit the file to your repository**: Use `git commit` to take a snapshot of your staged changes. The `-m` flag allows you to add a commit message, which should describe what changes were made.

    ```
    git commit -m "Add hello_git.py"
    ```

**Final Note**: The term "staging area" in Git is where you prepare your changes before committing them to your project's history. By using `git add` or `git stage`, you tell Git which changes you want to include in the next commit. This allows for more granular control over your project's version history, enabling you to commit only the changes that are ready, while continuing to work on other modifications.

![Git Locations](https://miro.medium.com/v2/resize:fit:686/1*diRLm1S5hkVoh5qeArND0Q.png "Git Locations")

## Understanding Branches

Branches are essential for managing different lines of development. They allow you to work on new features, bug fixes, or experiments in isolation from the main codebase.

### The "main" Branch

The "main" branch (formerly known as "master" in many repositories) is the default branch created when you initialize a new Git repository. It is considered the primary branch where the source code's current working version is maintained. Changes in this branch are usually the result of merging feature branches once they are complete and tested.

### Creating a New Branch

1. **Create a branch named `feature`**: Branches help you separate new development from stable code. The `git branch` command followed by a branch name creates a new branch.

    ```
    git branch feature
    ```

2. **Switch to the `feature` branch**: To start working on this branch, use `git checkout` with the branch name. You are now in an isolated environment to make changes.

    ```
    git checkout feature
    ```

### Making Changes in a Branch

1. **Edit your script**: Add a new feature or message in the `hello_git.py` script. This demonstrates how changes can be made in a branch without affecting the main branch.

    ```
    echo "print('Hello, Git! Welcome to the feature branch.')" > hello_git.py
    ```

2. **Add and commit your changes**: Like before, use `git add` and `git commit` to stage and commit your changes. Commit messages should reflect the development done in this branch.

    ```
    git add hello_git.py
    ```
    
    ```
    git commit -m "Update hello_git.py with a new feature"
    ```

### Viewing Branches and Their Relationships

To see what branch is the most ahead, or to understand the relationships between branches (including tags), you can use the following commands:

- **List all branches**: This command shows all branches in your repository. The current branch will be marked with an asterisk.

    ```
    git branch
    ```

- **List branches with commit details**: To see the latest commit on each branch, use:

    ```
    git branch -v
    ```

- **Show all branches and their upstreams**: This includes information about which branch is tracking which upstream branch (useful for knowing what will happen on `git push` and `git pull`).

    ```
    git branch -vv
    ```

- **Graphical representation of the branch history**: To see a graphical representation of the commit history across different branches, including tags, use:

    ```
    git log --graph --oneline --all
    ```

This command combines several options: `--graph` generates a text-based graphical representation, `--oneline` condenses each commit to a single line making it easier to read, and `--all` shows all branches, not just the current one.

### Conclusion

Understanding how to create and manage branches in Git allows you to work on various aspects of your project in parallel. The "main" branch serves as the backbone of your project, holding the most stable and updated version of your code. Using branches effectively is key to a successful version control strategy.


![image](https://github.com/augustross3/gittut/assets/98359182/0463d339-94a4-469b-a82e-3578500145c8)


## Merging Branches

Merging is the process of integrating changes from one branch into another. It's a common practice to merge a feature branch back into the main branch once development is complete.

1. **Switch to the `main` branch**: Before merging, you need to be on the branch that will receive the changes. Use `git checkout` to switch to the `main` branch.

```
git checkout main
```

2. **Merge the `feature` branch into `main`**: Use `git merge` followed by the name of the branch you want to merge. This command combines the histories of the `feature` branch and the `main` branch.

```
git merge feature
```

If there are no conflicts, your changes from the `feature` branch are now part of the main branch.

## Handling Merge Conflicts

Merge conflicts occur when Git is unable to automatically resolve differences in code between two commits. If you're merging a feature branch into the main branch and both branches have changes that conflict, you will need to manually resolve these conflicts.

### Understanding Merge Conflicts

When Git encounters a conflict during a merge, it will pause the merge process and mark the file as conflicted. Git also modifies the content of the conflicted files to show the areas of conflict, allowing you to manually review and resolve them.

### Resolving Merge Conflicts

1. **Identify conflicted files**: Git will list the files that have conflicts after attempting a merge. You can also use `git status` to see which files need resolution.

```
git status
```

2. **Edit the conflicted files**: Open the conflicted files in your favorite editor. Git marks the conflicts in the file like this:

```plaintext
<<<<<<< HEAD
// Version of the code in the current branch
=======
// Version of the code from the branch being merged in
>>>>>>> feature
```

You need to decide which version of the code to keep or merge the changes manually.

3. **Mark the conflict as resolved**: After editing the file to resolve the conflict, save your changes. Then, add the file to the staging area to mark it as resolved.

```
git add <filename>
```

4. **Complete the merge**: Once all conflicts are resolved and the changes are staged, you can complete the merge process by committing.

```
git commit
```

Git will open an editor to allow you to edit the commit message for the merge. By default, it includes a message indicating which merge was made. You can modify this message if you like, then save and exit the editor to complete the commit.

### Tips for Handling Merge Conflicts

- **Keep your branches up to date**: Regularly pulling changes from the main branch into your feature branch can help minimize conflicts.
- **Use a graphical merge tool**: Many graphical tools can help visualize and resolve conflicts more easily than editing the files directly.
- **Communicate with your team**: If you're working in a team and encounter conflicts, it's often helpful to discuss them with the person who made the conflicting changes.

Merge conflicts are a normal part of working with Git, especially on larger projects with multiple contributors. By understanding how to resolve these conflicts, you can ensure that your project's integration process is smooth and efficient.

## Pushing and Pulling Changes with Git

Once you've committed changes to your repository, you might want to share them with others or publish them to a remote repository like GitHub, GitLab, or Bitbucket. Likewise, you'll need to update your local repository with changes made by others. This is where the `git push` and `git pull` commands come into play.

### Pushing Changes to a Remote Repository

**Pushing** is the act of sending your local commits to a remote repository. It's how you share your work with others.

1. **Add a remote repository** (if you haven't already): Before you can push your changes, you need to specify the remote repository where you want to push your changes.

```
git remote add origin <repository-url>
```

Replace `<repository-url>` with the URL of your remote repository.

2. **Push your changes**: Use the `git push` command to send your changes to the remote repository.

```
git push origin main
```

This command pushes the changes from your local `main` branch to the `main` branch of the remote repository named `origin`. If you're working on a different branch, replace `main` with the name of your branch.

### Pulling Changes from a Remote Repository

**Pulling** is the process of fetching changes from a remote repository and merging them into your local branch. It's how you update your local repository with changes made by others.

1. **Pull the latest changes**: Use the `git pull` command to fetch and merge changes from the remote repository into your current branch.

```
git pull origin main
```

This command fetches changes from the `main` branch of the remote repository named `origin` and merges them into your current local branch.

### Handling Merge Conflicts During Pull

Similar to merging branches locally, pulling changes from a remote repository can also result in merge conflicts if both your local repository and the remote repository have diverging changes. If this happens, you'll need to resolve the conflicts in the same way you would resolve merge conflicts between branches locally.

### Best Practices for Pushing and Pulling

- **Frequent, small pushes**: Instead of accumulating a lot of changes and pushing them all at once, push small changes frequently. This reduces the risk of conflicts and makes it easier to manage your code.
- **Pull before you push**: Before pushing your changes, it's a good practice to `pull` the latest changes from the remote repository. This ensures that your local branch is up-to-date and can help avoid conflicts.


## Conclusion

You've now covered the fundamentals of using Git for version control, including setting up repositories, making commits, working with branches, and merging changes. These skills are crucial for effective collaboration and project management in software development.
