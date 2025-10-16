LeMiCi-assignment

1-Done
2-   git fetch downloads the latest changes from the remote repository to your local repo's remote tracking branches but it does not change your current working files or branches. It just allows you to see       what's new before merging.
     git pull is a combination of git fetch followed immediately by git merge. It fetches changes and automatically merges them into your current branch, which can sometimes lead to merge conflicts.

     Example steps to resolve Merge conflicts:
     Merge conflicts occur when changes in two different branches conflict on the same lines.
     first of all identify conflict markers (<<<<<<<, =======, >>>>>>>) in files.
     Then manually edit the file to resolve the conflicting changes.
     Add the resolved file: git add <filename>.
     Then complete the merge by committing it
3-
