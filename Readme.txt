This project demonstrates how to use SourceTree (a Git client) to:
- Reverse a commit
- Reset a branch to a commit
- Undo a merge


Reverse a commit
================
This creates a new commit which undoes the changes in the previous commit. The commits still appear in the commit history. Only the changes are reversed.
Method:
- Select the commit you want to reverse.
- Right-click and select 'Reverse commit'.


Reset a branch to a commit
==========================
This completely removes commits from the repository. Any commits past the selected point no longer appear in the repository.
Method:
- Select the commit you want to 'roll back' to. Any commits past this point will cease to exist.
- Right-click and select 'Reset [branch name] to this commit'.


Undo a merge by reversing a commit
==================================
When you attempt to use the 'reverse a commit' method to undo a merge, you'll get the following error:
    git -c diff.mnemonicprefix=false -c core.quotepath=false -c credential.helper=sourcetree revert --no-edit 238776da23c11151cd4181a6944352f0418ceb1f
    error: Commit 238776da23c11151cd4181a6944352f0418ceb1f is a merge but no -m option was given.
    fatal: revert failed
    Completed with errors, see above'
Resolution: Follow the technique here: http://stackoverflow.com/questions/35652427/git-reverse-commit-a-pushed-merge-in-sourcetree


Undo a merge by resetting to a commit
=====================================
You can use the technique described in 'Reset a branch to a commit' to reverse a merge and discard the commit history.
If you pushed to the remote, you may need to follow: http://stackoverflow.com/questions/35652427/git-reverse-commit-a-pushed-merge-in-sourcetree

Working with remotes
====================
When you've already pushed the changes to the remote, and'you try to use git to 'revert to a commit', it will work locally, but the status goes back to before the 'revert' operation if you 'pull' from the remote. This is because the 'revert to commit' applies the changes locally by deleting history. The remote is not aware of this. You need to force the remote to accept the local changes by using Terminal.
Need to use: git push origin NAME_OF_BRANCH --force
    E.g. 'git push origin branchA --force'
This forces the remote to accept the local changes.
