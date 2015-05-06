## Git Gists

### Auto Commit

    $ git commit -a -m "Commit message"

### Visual History

    $ git log --graph --oneline --all --decorate

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
