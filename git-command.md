# Default Branch Name
git config --global init.defaultBranch main


git add <file> - Stage a file
git add --all or git add -A - Stage all changes
git status - See what is staged
git restore --staged <file> - Unstage a file // git rm --cached git-command.md  


git commit -m "message" - Commit staged changes with a message
git commit -a -m "message" - Commit all tracked changes (skip staging)
git log - See commit history



# Commit Message Best Practices:
    Keep the first line short (50 characters or less).
    Use the imperative mood (e.g., "Add feature" not "Added feature").
    Leave a blank line after the summary, then add more details if needed.
    Describe why the change was made, not just what changed.

# Other Useful Commit Options

    Create an empty commit:
    git commit --allow-empty -m "Start project"
    Use previous commit message (no editor):
    git commit --no-edit
    Quickly add staged changes to last commit, keep message:
    git commit --amend --no-edit


# For a shorter view
git log --oneline

# To see which files changed in each commit
git log --stat

# Key Commands for Tagging

    git tag <tagname> - Create a lightweight tag
    git tag -a <tagname> -m "message" - Create an annotated tag
    git tag <tagname> <commit-hash> - Tag a specific commit
    git tag - List tags
    git show <tagname> - Show tag details

# Tagging Best Practices

    Use tags to mark releases, major milestones, or stable points in your project.
    Always use annotated tags (with -a -m) for anything public or shared.
    Create tags after passing all tests or before deploying/releasing code.



# Push All Tags
git push --tags

# Delete a tag locally
git tag -d v1.0

# Delete a tag from the remote repository
git push origin --delete tag v1.0

# If you need to move a tag to a different commit and update the remote
git tag -f v1.0 <new-commit-hash>
git push --force origin v1.0


# Key Commands for Stashing

    git stash - Stash your changes
    git stash push -m "message" - Stash with a message
    git stash list - List all stashes
    git stash branch <branchname> - Create a branch from a stash


# What is Git Stash? Why Use It?

Sometimes you need to quickly switch tasks or fix a bug, but you're not ready to commit your work.

git stash lets you save your uncommitted changes and return to a clean working directory.

You can come back and restore your changes later.

Here are some common use cases:

    Switch branches safely: Save your work before changing branches.
    Handle emergencies: Stash your work to fix something urgent, then restore it.
    Keep your work-in-progress safe: Avoid messy commits or losing changes.

# What gets stashed?

    Tracked files (both staged and unstaged) are stashed by default.
    Untracked files (new files not yet added to Git) are not stashed by default.
    To stash untracked files too, use git stash -u (or --include-untracked).

# Best Practices for Stashing

    Use clear messages when stashing: git stash push -m "WIP: feature name"
    Don't use stashes as long-term storage-commit your work when possible.
    Check your stash list regularly and clean up old stashes you no longer need.

# Best Practices for Working with Branches

    Use clear, descriptive branch names (like feature/login-page or bugfix/header-crash).
    Keep each branch focused on a single purpose or feature.
    Regularly merge changes from the main branch to keep your branch up-to-date.
    Delete branches that are no longer needed to keep your repository clean.

The Three Areas of Git

    Working Directory: Where you make changes to your files.
    Staging Area (Index): Where you prepare changes before committing.
    Repository: Where your committed history is stored.

Workflow Diagram
[Working Directory] --git add--> [Staging Area] --git commit--> [Repository]