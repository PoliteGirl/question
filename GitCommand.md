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

### Q :How do you delete a branch in Git?
You can delete a branch using the git branch -d command.

### Q : To rename a file
git mv
