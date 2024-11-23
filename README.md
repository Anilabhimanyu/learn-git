
# Learn Git Repository

## Purpose
This repository is designed to help to learn Git from scratch to advanced levels. It includes exercises, documentation, and examples for each Git concept.

## Structure
The repository is organized into sections to focus on specific Git concepts:
1. **Setup-and-Basics**: Initial setup and basic Git commands.
2. **Version-Control**: File version management and history tracking.
3. **Branching**: Working with branches for feature development.
4. **Remote-Repositories**: Collaborating with remote repositories.
5. **Advanced-Commands**: Exploring advanced Git techniques.
6. **Collaboration**: Simulating team workflows and resolving conflicts.
7. **Tips-and-Tricks**: Handy shortcuts and best practices.

---

## Getting Started

### Clone This Repository
```bash
git clone https://github.com/Anilabhimanyu/learn-git.git
cd learn-git
```

### Explore the Repository
Each section contains clear instructions for hands-on practice.

---

## Setup-and-Basics

Install Git:
```bash
sudo apt install git       # Ubuntu/Debian
brew install git           # macOS
git --version              # Check version
```

Initial Configuration:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --list          # Verify configuration
```

Start a New Repository:
```bash
mkdir my-project
cd my-project
git init
echo "Hello Git" > README.md
git add README.md
git commit -m "Initial commit"
```

**Notes:**
- `--global`: Applies to all repositories for the user.
- `--local`: Applies only to the current repository.
- `--system`: System-wide configuration.

---

## Version-Control

Check Changes:
```bash
git status
git diff                  # Show unstaged changes
git diff --staged         # Show staged changes
```

Track and Commit Changes:
```bash
git add filename          # Stage a file
git add .                 # Stage all files
git commit -m "Message"   # Commit changes
```

Undo Changes:
```bash
git reset filename        # Unstage a file
git checkout -- filename  # Revert unstaged changes
git reset --hard HEAD~1   # Undo the last commit
```

**Notes:**
- `git reset`: Moves the HEAD pointer. Use cautiously.
- `git revert`: Creates a new commit that undoes changes.
- `git checkout`: Restores a specific version or switches branches.

---

## Branching

Create and Switch Branches:
```bash
git branch feature-branch     # Create a branch
git switch feature-branch     # Switch to the branch
```

Merge Branches:
```bash
git switch main               # Switch to the main branch
git merge feature-branch      # Merge feature-branch into main
```

Delete Branches:
```bash
git branch -d feature-branch  # Delete a merged branch
git branch -D old-branch      # Force delete an unmerged branch
```

**Notes:**
- Merging keeps history, while rebasing rewrites it.
- Use `git stash` to save work without committing.

---

## Remote-Repositories

Add Remote Repository:
```bash
git remote add origin https://github.com/user/repo.git
```

Push Changes:
```bash
git push -u origin main       # Push main branch to remote
```

Pull Changes:
```bash
git pull origin main          # Pull changes from remote
```

List Remote Repositories:
```bash
git remote -v
```

---

## Advanced-Commands

Stash Changes:
```bash
git stash                   # Save current state without committing
git stash pop               # Apply the last stash
git stash list              # View all stashes
```

Rebase:
```bash
git rebase main             # Reapply commits on top of another branch
```

Cherry-Pick:
```bash
git cherry-pick commit-hash # Apply a specific commit to the current branch
```

---

## Collaboration

Simulate Team Workflow:
```bash
git fetch                   # Fetch remote updates
git merge                   # Merge updates into the current branch
```

Resolve Conflicts:
- Open conflicting files and edit.
- Stage resolved files:
    ```bash
    git add filename
    ```
- Commit changes:
    ```bash
    git commit
    ```

---

## Tips-and-Tricks

- Use `git log --oneline --graph` to visualize branch history.
- Use `.gitignore` to exclude files from version control.
- Use `git blame filename` to find commit history for each line.
- Use `git bisect` to identify problematic commits.

---

Happy Git Learning!

This format ensures every section looks great in GitHub and maintains readability. Copy-paste this into your `README.md`!

## Scenario Based Questions
### 1. **Branching Strategy**
#### **Scenario:**
You are working on a feature branch called `feature/new-dashboard` for a new UI component. However, while working on the feature, your team needs to apply a critical bug fix to the `main` branch. You are behind on the `main` branch and need to update your feature branch with the latest changes without affecting your work.

#### **Question:**  
How would you handle this situation?

#### **Answer:**  
You can update your feature branch with the latest changes from `main` by using `git fetch` followed by `git rebase`. This keeps your branch updated without creating a merge commit. Here are the steps:
1. `git fetch origin` — Fetch the latest changes from the remote.
2. `git rebase origin/main` — Rebase your feature branch on top of the latest `main` branch.
3. Resolve any conflicts that arise, then continue the rebase with `git rebase --continue`.
4. Push your updated branch using `git push origin feature/new-dashboard`.

---

### 2. **Merge Conflicts**
#### **Scenario:**
You and a colleague have both made changes to the same file in different branches. When you try to merge your feature branch into the `main` branch, a merge conflict arises.

#### **Question:**  
How would you resolve this conflict, and what steps would you take to ensure that the conflict is handled properly?

#### **Answer:**  
To resolve a merge conflict:
1. After the conflict appears, Git will mark the conflicting files. Open the conflicting files and look for the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
2. Decide which changes to keep and remove the conflict markers.
3. Stage the resolved files with `git add <file>`.
4. Complete the merge with `git merge --continue` or if rebasing, use `git rebase --continue`.
5. Finally, push your changes with `git push`.

---

### 3. **Undoing Changes**
#### **Scenario:**
You committed a change to the wrong branch. You realized this mistake after committing it, and you need to move that commit to the correct branch.

#### **Question:**  
What Git commands would you use to resolve this?

#### **Answer:**  
To undo the commit on the wrong branch and move it to the correct one:
1. Use `git reset HEAD~1` to unstage the last commit.
2. Checkout the correct branch with `git checkout correct-branch`.
3. Use `git cherry-pick <commit-id>` to apply the commit to the correct branch.
4. Finally, push the changes to the correct branch.

---

### 4. **Working with Remote Repositories**
#### **Scenario:**
You have cloned a repository and made some local changes. Before pushing your changes to the remote repository, someone else has pushed changes to the same branch you are working on.

#### **Question:**  
How would you proceed to incorporate the latest remote changes into your local branch before pushing your own?

#### **Answer:**  
To incorporate remote changes into your local branch:
1. Use `git fetch origin` to get the latest changes from the remote repository.
2. Then, rebase your local branch on top of the remote branch with `git rebase origin/<branch-name>`.
3. Resolve any conflicts, if necessary.
4. Finally, push your changes using `git push`.

---

### 5. **Rewriting History**
#### **Scenario:**
You committed several changes to your local branch, but some of these commits contain sensitive information (like passwords or API keys). You want to remove these commits from history.

#### **Question:**  
How would you rewrite your commit history to remove the sensitive information from the Git history?

#### **Answer:**  
To remove sensitive information from Git history:
1. Use `git rebase -i HEAD~n` to interactively rebase the last `n` commits.
2. Mark the commits containing sensitive data with `edit` and remove the sensitive information.
3. Once the changes are made, use `git commit --amend` to amend the commit.
4. Complete the rebase with `git rebase --continue`.
5. Force-push the changes using `git push --force` to overwrite the history on the remote.

---

### 6. **Stashing Changes**
#### **Scenario:**
You are working on a feature but need to quickly switch to a different task to review a bug that needs immediate attention. You haven't finished your current task, and there are uncommitted changes.

#### **Question:**  
How would you handle this situation in Git so that you can come back to your feature work later?

#### **Answer:**  
You can stash your changes temporarily with the following commands:
1. `git stash` — Stash the current changes.
2. Switch to the other branch with `git checkout <branch>`.
3. Once the task is complete, return to your original branch with `git checkout <feature-branch>`.
4. Apply your stashed changes with `git stash pop`.

---

### 7. **Git Hooks**
#### **Scenario:**
You need to automate some tasks in your Git workflow, such as running unit tests before each commit to ensure the codebase isn't broken.

#### **Question:**  
Which Git hook would you use, and how would you set it up?

#### **Answer:**  
You can use the `pre-commit` hook. It’s triggered before a commit is made, allowing you to run tests or linters:
1. Create a `.git/hooks/pre-commit` file in your repository.
2. Add a script to run unit tests or any checks.
3. Ensure the script is executable using `chmod +x .git/hooks/pre-commit`.

---

### 8. **Rebasing vs Merging**
#### **Scenario:**
Your team has a policy of using `git rebase` for keeping feature branches up-to-date with the `main` branch, but you prefer using `git merge`.

#### **Question:**  
What are the pros and cons of using `git rebase` versus `git merge`, and how would you explain this to your team?

#### **Answer:**  
- **Rebase:** 
  - **Pros:** Creates a cleaner history by avoiding unnecessary merge commits.
  - **Cons:** Rewriting commit history can cause issues when shared with others.
- **Merge:** 
  - **Pros:** Preserves history and is safer for shared branches.
  - **Cons:** Creates more merge commits, leading to a potentially cluttered history.
- For feature development, `rebase` is often preferred for cleaner history, but use `merge` when collaborating with others.

---

### 9. **Fast-Forward Merge**
#### **Scenario:**
You have been working on a feature branch and want to merge it into the `main` branch. The `main` branch hasn't changed since you created your feature branch.

#### **Question:**  
What type of merge will Git perform, and what steps would you take to complete the merge?

#### **Answer:**  
In this case, Git will perform a **fast-forward merge** because no new commits exist on `main` since you branched off. To complete the merge:
1. Checkout the `main` branch: `git checkout main`.
2. Merge the feature branch: `git merge feature-branch`.
3. Git will fast-forward without creating a merge commit.

---

### 10. **Commit Squashing**
#### **Scenario:**
You have made several small commits during the development of a feature, but you want to clean up the commit history before merging it into the `main` branch. You want to squash all the commits into a single commit.

#### **Question:**  
How would you achieve this, and when would you use this approach?

#### **Answer:**  
To squash commits:
1. Use `git rebase -i HEAD~n` where `n` is the number of commits to squash.
2. In the editor, change the word `pick` to `squash` for all but the first commit.
3. After saving and closing the editor, Git will combine the commits into one.
4. Push the changes using `git push --force`.

Squashing is useful for keeping the commit history clean by combining related commits into a single logical commit before merging.

---

### 11. **Git Submodules**
#### **Scenario:**
Your team is working with a shared library that is stored in a separate Git repository. You want to include this repository inside your project so that it's treated as a submodule.

#### **Question:**  
How would you add this submodule to your Git repository, and what are the important considerations when working with Git submodules?

#### **Answer:**  
To add a submodule:
1. Use `git submodule add <repository-url> <path-to-submodule>`.
2. Commit the change to your repository: `git commit -m "Added submodule"`.
3. Push the changes to the remote.

Considerations:
- Submodules are tracked by commit hash, not the latest branch.
- You need to update the submodule with `git submodule update` if changes are made to the submodule repository.

---

### 12. **Rollback to Previous Commit**
#### **Scenario:**
After pushing your changes to a shared repository, you realize that the latest commit has introduced a bug into the application, and you need to roll back to the previous stable commit.

#### **Question:**  


## Conclusion
This repository serves as a hands-on guide to mastering Git. By working through these scenarios, you will better understand how Git works in real-world situations, manage source code effectively, and collaborate with teams more efficiently.
