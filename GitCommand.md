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

* git merge = git fetch + git merge

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
one thing you can do is fix and remove bad file in previous commit and the commit that change and push that code.

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

### Q : How do you delete a branch in Git?
You can delete a branch using the git branch -d command.

### Q : To rename a file
```
git mv <source> <destination>
git mv oldfile.txt newfile.txt
```

### Q : How to find a list of file that has been changed in a commit
git diff-tree -r {commit id}

### Q : Config command
It is use to change git username and email
git config --global user.name "name"
git config --global user.email "email"

### Q : Check which branch already merged in current branch
git branch --merged
git branch --no-merged

### Q : What is git cherry-pick?
git cherry-pick is a Git command that allows you to apply a specific commit from one branch to another. It essentially lets you choose a commit from one branch and apply it onto another branch, bringing the changes made in that commit to the target branch.

The basic syntax for git cherry-pick is:
```
git cherry-pick <commit_hash>
```
Example:
Suppose you have a branch named feature_branch with a commit identified by abc123 that contains changes you want to bring into your main branch. You would execute:
```
git checkout main
git cherry-pick abc123
```

This would apply the changes made in the abc123 commit from feature_branch onto the main branch.

git cherry-pick is useful for selectively bringing changes from one branch to another, especially when merging branches or backporting specific fixes.

### Q : Diff beetween revert and reset
Both git revert and git reset are commands in Git used to undo changes, but they have different purposes and implications.

* git revert:
Purpose: Creates a new commit that undoes the changes made in a previous commit. It's a safe way to undo changes while preserving the commit history.
```
git revert <commit_hash>

git revert abc123
```
Effect: Generates a new commit that undoes the changes introduced by the specified commit. It does not remove the original commit but adds a new commit that negates its changes.

* git reset:
Purpose: Resets the current branch to a specified commit, discarding changes or moving the branch pointer to a different commit. It's a more forceful operation that can rewrite history.
```
git reset <commit_hash> --soft|mixed|hard
```

--soft: Preserves changes in the working directory and staging area.
--mixed (default): Preserves changes in the working directory but not in the staging area.
--hard: Discards changes in the working directory, staging area, and reverts the branch to the specified commit.
Effect: Depends on the chosen reset mode. It can move the branch pointer and reset the staging area and working directory accordingly. --hard can be used to discard changes entirely.

* In summary:

Use git revert to create a new commit that undoes the changes of a specific commit while preserving history.
Use git reset to move the branch pointer and potentially discard changes. Be cautious with --hard as it can permanently remove changes.
In general, git revert is safer for undoing changes in shared repositories, especially when working collaboratively, as it maintains a clear and traceable history. On the other hand, git reset can be more aggressive and is often used for local, private branches when you need to rework or discard changes.

## Docker
Certainly! Here's a beginner-friendly guide to Docker, covering the basics and essential concepts:

### What is Docker?

**Docker** is a platform that allows you to develop, deploy, and run applications in containers. Containers are lightweight, portable, and self-sufficient environments that encapsulate an application and its dependencies.

### Key Concepts:

1. **Images:**
   - Docker images are the blueprints for containers. They contain the application code, libraries, dependencies, and other configurations needed to run the application.

2. **Containers:**
   - Containers are instances of Docker images. They are isolated environments that run applications. Containers are portable and consistent across different environments.

### Docker Installation:

1. **Install Docker Desktop:**
   - Download and install Docker Desktop from the official website (https://www.docker.com/products/docker-desktop) based on your operating system.

2. **Verify Installation:**
   - Open a terminal or command prompt and run:
     ```bash
     docker --version
     docker run hello-world
     ```

### Basic Docker Commands:

1. **Build an Image:**
   - Create a Dockerfile in your project directory and build an image.
     ```Dockerfile
     FROM node:14
     WORKDIR /app
     COPY . .
     CMD ["npm", "start"]
     ```
     ```bash
     docker build -t my-node-app .
     ```

2. **Run a Container:**
   - Start a container from the image.
     ```bash
     docker run -p 4000:3000 my-node-app
     ```

3. **List Running Containers:**
   - View the list of running containers.
     ```bash
     docker ps
     ```

4. **Stop a Container:**
   - Stop a running container.
     ```bash
     docker stop <container_id>
     ```

5. **Remove a Container:**
   - Remove a stopped container.
     ```bash
     docker rm <container_id>
     ```

6. **List Images:**
   - View the list of locally available images.
     ```bash
     docker images
     ```

7. **Remove an Image:**
   - Remove an image.
     ```bash
     docker rmi <image_id>
     ```

### Additional Concepts:

1. **Docker Compose:**
   - Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file to configure application services, networks, and volumes.

2. **Volumes:**
   - Docker volumes allow you to persist data outside of containers. They provide a way to share data between a host machine and containers.

3. **Networking:**
   - Docker provides networking features to allow containers to communicate with each other. Containers can be connected to custom networks to control their communication.

### Resources for Learning:

1. **Docker Documentation:**
   - [Docker Documentation](https://docs.docker.com/)
   - The official documentation provides comprehensive guides and references.

2. **Docker Tutorial for Beginners:**
   - [Docker Tutorial for Beginners](https://www.tutorialspoint.com/docker/index.htm)
   - A step-by-step tutorial covering Docker basics.

3. **Docker Cheat Sheet:**
   - [Docker Cheat Sheet](https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf)
   - A handy cheat sheet with commonly used Docker commands.

Dive into these resources, practice with simple applications, and gradually explore more advanced Docker features as you become comfortable with the basics.
