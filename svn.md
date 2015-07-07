## SVN Gists

### Check for remote changes

    $ svn st --show-updates

### Comparing files

Compare differences of a file between specific revisions

    $ svn diff -r 8:10 http://svn.host.com/path/to/file.txt

Compare local changes to specific revision

    $ svn diff -r 8

### Svn info

    # what branch am I working from
    $ svn info | grep URL
    $what revision am I working on
    $ svn info | grep Revision

    # show last three commits
    $ svn log -l 3

### Revert a file

    $ svn revert /path/to/file

    # revert back to specific revision (current revision 10 back to revision 8)
    $ svn merge -r 10:8 .

### Branching

Create a new branch

    $ svn cp http://svn.host.com/path/to/project/trunk \
        http://svn.host.com/path/to/project/branches/BRANCH_NAME \
        -m "Branching from trunk to BRANCH_NAME at r#"

Switch local repo to branch

    $ svn switch http://svn.host.com/path/to/project/branches/BRANCH_NAME

Switching between branches/trunk

    $ svn switch http://svn.host.com/path/to/project/trunk

### Merging

Merge any changes into branch from latest revision of trunk

    $ svn merge http://svn.host.com/path/to/project/trunk .

    # merge any changes into branch since revision 2 from trunk revision 8
    $ svn merge -r 2:8 http://svn.host.com/path/to/project/trunk .

If problems occur, revert back to previous revision using the revert command

    $ svn revert -R .

Merging a completed branch into trunk

    # after switching local repo to trunk
    $ svn merge --reintegrate http://svn.host.com/path/to/project/branches/BRANCH_NAME

    # commit trunk with new branch
    $ svn commit -m "Merged BRANCH_NAME back into trunk"

    # optionally, remove branch
    $ svn delete http://svn.host.com/path/to/project/branches/BRANCH_NAME -m "Removed branch BRANCH_NAME, reintegrated into trunk in r#"