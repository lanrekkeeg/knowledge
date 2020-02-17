
# Git

## Completely throws away all your uncommitted changes

```
git reset --hard HEAD
```

## Remove untracked files

```
git clean -df
```

**CAUTION:** As above but removes ignored files, like IDE configurations:

```
git clean -xdf
```

## Filename too long (Windows)

In command-prompt (with administrative rights), you should be able to run the command:

```
git config --system core.longpaths true
```

## Push local branch to another remote branch

```
git push origin <local-name>:<remote-name>
```

## Reset to current master

```
git reset origin/master
```

## Checkout Custom Remote Branch

```
git checkout -b public/master --track public/master
```

## Rename Remote Branch

```
git checkout name_of_the_old_branch_on_github
git push origin :name_of_the_old_branch_on_github
git checkout -b my_new_name
git push origin my_new_name
```

## Store Credentials

```
git config --global credential.helper store
```

## Fix Git LFS Issues

> Fix "Encountered 1 file(s) that should have been pointers, but weren't" issue, see <https://github.com/git-lfs/git-lfs/issues/2910>.

```
git rm --cached <file>
git add --force <file>
git commit -m "Move files properly to GitLFS"
```

## Reset vs. Revert

`git revert` undoes a commit by creating a new commit.
`git revert` should be used to undo changes on a public branch, and `git reset` should be reserved for undoing changes on a private branch.
You can also think of `git revert` as a tool for undoing committed changes, while `git reset HEAD` is for undoing uncommitted changes.

| Command      | Scope        | Common use cases |
| ------------ | ------------ | ---------------- |
| `git reset` | Commit-level | Discard commits in a private branch or throw away uncommited changes |
| `git reset` | File-level   | Unstage a file |
| `git checkout` | Commit-level | Switch between branches or inspect old snapshots |
| `git checkout` | File-level   | Discard changes in the working directory |
| `git revert` | Commit-level | Undo commits in a public branch |

## Rebase vs. Merge

Both of these commands are designed to integrate changes from one branch into another branch - they just do it in very different ways.

### Checkout a feature branch and merge the current master

```
git checkout feature
git merge master
```

This creates a merge commit and is a non-destructive operation.
If your master is very active, this will result in a lot of merge commits and pollutes your feature branch history quite a bit.

### The `git rebase` option

**The Golden Rule of Rebasing:** Never use `git rebase` on public branches, like `master`.

Always ask yourself, "Is anyone else looking at this branch?"
If the answer is yes, take your hands off the keyboard and start thinking about a non-destructive way to make your changes (e.g., the `git revert` command).
Otherwise, you're safe to re-write history as much as you like.

```
git checkout feature
git rebase master
```

This moves the entire feature branch in front of the master branch, effectively incorporating all of the new commits in master.
Rebasing re-writes the project history by creating brand new commits for each commit in the original branch.
You get a much cleaner history, no merge commits and a perfectly linear project history.

### Interactive Rebasing

Interactive rebasing gives you the opportunity to alter commits as they are moved to the new branch.
Typically, use it to clean up a messy history before merging a feature branch into master.

```
git checkout feature
git rebase -i master
```

This will open a text editor listing all of the commits that are about to be moved:

```
pick 33d5b7a Message for commit #1
pick 9480b3d Message for commit #2
pick 5c67e61 Message for commit #3
```

By using the `fixup` command (instead of `pick`) and/or re-ordering the entries, you can make the branch's history look like whatever you want.
For example, if the 2nd commit fixes a small problem in the 1st commit, you can condense them into a single commit with the `fixup` command:

```
pick 33d5b7a Message for commit #1
fixup 9480b3d Message for commit #2
pick 5c67e61 Message for commit #3
```

### Integrating an Approved Feature

If you are not entirely comfortable with `git rebase`, you can always perform the rebase in a temporary branch.
That way, if you accidentally mess up your feature's history, you can check out the original branch and try again.

For example:

```
git checkout feature
git checkout -b temporary-branch
git rebase -i master
# [Clean up the history]
git checkout master
git merge temporary-branch
```

### Rebasing a Remote Branch

```
git checkout feature
git pull --rebase origin master
git push origin feature -f
```

## Using Git behind a Proxy Server

Put the following to your `.gitconfig` file:

```
[http]
  proxy = http://your-proxy-server.com:8088
[https]
  proxy = http://your-proxy-server.com:8088
[url "https://"]
  insteadOf = git://
```

## Links

- [Writing Good Commit Messages](> https://github.com/erlang/otp/wiki/writing-good-commit-messages)
