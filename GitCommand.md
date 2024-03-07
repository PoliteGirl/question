# Git Question

### Q : What is Git?
A : Git is a distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

### Q : Explain the basic Git workflow.
The basic Git workflow involves creating a repository, making changes to files, staging those changes, committing them, and pushing the changes to a remote repository.

### Q : What is a repository in Git?
A Git repository is a storage location where your project's history and source code are stored. It can be local or remote.

### Q : How do you create a new Git repository?
You can create a new Git repository using the git init command.

### Q : Explain the difference between Git and GitHub.
Git is a version control system, while GitHub is a web-based platform for hosting Git repositories and collaboration.

### Q : What is a commit in Git?
A commit is a snapshot of the changes made to a Git repository. It represents a point in the project's history.

### Q : How do you check the status of your current Git repository?
You can use the git status command to see the status of your working directory and staging area.

### Q : Explain the difference between Git pull and Git fetch.
git pull fetches changes from a remote repository and merges them into the current branch, while git fetch only fetches changes but doesn't merge them.

### Q : Explain the Git rebase command.
git rebase is used to combine a sequence of commits into a new base commit. It's often used to keep the commit history linear and clean.

Git rebase is a command used to reapply commits on top of another branch, essentially rewriting the commit history. It's a powerful tool for incorporating changes from one branch onto another while keeping a linear commit history.

The basic syntax for a rebase is:
```
git rebase <base_branch>
```
Here, <base_branch> is the branch onto which you want to rebase your current branch. When you perform a rebase, Git will take the commits unique to your current branch (not found in the <base_branch>) and reapply them on top of <base_branch>.

For example, if you're currently on a feature branch feature_branch and you want to rebase it onto the main branch, you would execute:
```
git checkout feature_branch
git rebase main
```
After this command, Git will replay the commits from feature_branch on top of main, effectively incorporating the changes from main into your feature branch.

Rebasing is commonly used in workflows to keep a clean and linear commit history. It's often preferred over merging because it avoids unnecessary merge commits, resulting in a more readable and understandable history. However, rebasing should be used with caution, especially when working in a collaborative environment, as it can rewrite history and potentially cause conflicts for other team members.

### Q : How do you undo or revert the last Git commit?
You can use the git reset or git revert command to undo the last Git commit. The choice depends on whether the commit has been pushed to a remote repository.
```
git revert <commit id>
```

### Q : To check history of commit
git log = it will give previous commit history with commit id, Author, Date

### Q : What is Git bisect used for?
git bisect is a command used for binary searching through the commit history to find the commit where a bug was introduced.

### Q : Explain the Git stash command.
git stash is used to save changes that are not ready to be committed yet but need to be set aside temporarily. It allows you to switch branches without committing changes.

that are not ready to be committed. This can be useful in scenarios where you want to switch to a different branch, apply some changes, or simply set aside your current modifications without committing them.

The basic usage of git stash involves two main operations: stashing changes and later applying them.

* Stash Changes:
To stash your changes, use the following command:
```
git stash save "Your stash message"
```
This command takes all the changes in your working directory (including staged and unstaged changes) and saves them in a new stash. The optional message is a description of the stash, which can be helpful for future reference.

* List Stashes:
You can view a list of your stashes using:
```
git stash list
```
This will show you a list of stashes, each with a unique identifier (e.g., stash@{0}, stash@{1}, etc.).

* Apply Stashed Changes:
To apply the stashed changes back to your working directory, you have a couple of options:

Apply the latest stash:
```
git stash apply
```
Apply a specific stash (identified by its reference, e.g., stash@{1}):
```
git stash apply stash@{1}
```
By default, applying a stash will leave the stash intact. If you want to remove the stash after applying, you can use:
```
git stash drop stash@{1}
```
Alternatively, you can combine the apply and drop operations using:
```
git stash pop
```
This will apply the changes and remove the latest stash.

* Clear All Stashes:
To remove all stashes, you can use:
```
git stash clear
```
The git stash command is handy when you need to switch branches, pull changes, or perform other operations that might conflict with your current changes. Stashing allows you to store your changes temporarily, switch to a different context, and later reapply the changes when needed.

### Q :How do you delete a branch in Git?
You can delete a branch using the git branch -d command.

### Q : To rename a file
```
git mv <source> <destination>
git mv oldfile.txt newfile.txt
```
