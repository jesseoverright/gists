## Git Gists

### Commits

Auto commit all changes

    $ git commit -a -m "Commit message"

Revert local changes

    $ git checkout -- /path/to/file

Amend most recent commit message

    $ git commit --amend -m "New Message"

### Visual History

Pretty graph of all branches

    $ git log --graph --oneline --all --decorate

Show diff of last commit 

    $ git log -p -1

### Rewrite History

Cherrypick and squash commits from the last 5 commits

    $ git rebase -i HEAD~5

### Branching

Switch to branch

    $ git checkout branchname

Checkout new branch

    $ git checkout -b new/branchname

Stashing changes

    $ git stash
    # pop out changes later
    $ git stash pop

### Links

- [Git branch details in bash prompt](http://code-worrier.com/blog/git-branch-in-bash-prompt/)
