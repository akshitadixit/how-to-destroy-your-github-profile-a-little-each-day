# Git Gaffes

## Introduction

Git is a powerful version control tool that has revolutionized the way we develop software. However, even the most experienced developers can make mistakes. This folder contains examples of humorous GitHub mistakes and blunders that have occurred over the years, along with commentary on each one. The purpose of this folder is to provide guidance on how to avoid similar mistakes while also providing a fun and lighthearted take on the topic.

## Examples

### Example 1: The Accidental Push

One of the most common Git Gaffes is accidentally pushing sensitive information to a public repository. This can happen when developers forget to add files to the `.gitignore` file, or when they accidentally include sensitive information in their code comments.

```bash
$ git push origin master
Counting objects: 17, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (17/17), done.
Writing objects: 100% (17/17), 2.58 KiB | 2.58 MiB/s, done.
Total 17 (delta 8), reused 0 (delta 0)
remote: Resolving deltas: 100% (8/8), completed with 3 local objects.
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: 90262f79291c36db29f1d60dd75e456e
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File app/libraries/aws/aws.phar is 125.20 MB; this exceeds GitHub's file size limit of 100.00 MB
To https://github.com/example/repo.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'https://github.com/example/repo.git'
```

The best way to avoid accidentally pushing sensitive information to a public repository is to be proactive. Before pushing any changes, double-check that you have:

- Updated your `.gitignore` file to exclude any sensitive files or folders.
- Removed any sensitive information from your code comments or commit messages.
- Reviewed your changes carefully to ensure that there are no accidental inclusions.

If you have already pushed sensitive information to a public repository, the first step is to remove it from the repository history. You can do this using the `git filter-branch` command:

```bash
$ git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch <file>" \
  --prune-empty --tag-name-filter cat -- --all
```
Once you have removed the sensitive information, you will need to force push the updated history to the remote repository:

    ```bash
    $ git push origin master --force
    ```


### Example 2: The Merge Mishap

Another common Git Gaffe is merging the wrong branch and accidentally deleting important code. This can happen when developers have multiple branches and forget to switch to the correct one before making changes.

```bash
$ git merge feature-branch
Auto-merging app.js
CONFLICT (content): Merge conflict in app.js
Automatic merge failed; fix conflicts and then commit the result.
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

    both modified:   app.js

no changes added to commit (use "git add" and/or "git commit -a")
$ git checkout feature-branch
$ git diff HEAD~1 app.js
-// Some important code
+// Deleted by mistake :(
```

The best way to avoid merging the wrong branch is to use Git's branch switching commands, such as `git checkout` or `git switch`, to switch between branches. Before making any changes, double-check that you are on the correct branch by running:

```bash
$ git branch
* master
  feature-branch
```

If you have already merged the wrong branch, you can use the `git reset` command to undo the merge and restore the previous state of the repository:

```bash
$ git reset --hard HEAD~1
HEAD is now at 3b0e5c1 Merge branch 'feature-branch'
```

or to undo the merge using the git merge --abort command:

```bash
$ git merge --abort
```
This will undo the merge and restore your repository to its previous state. If you have made any changes that you want to keep, you can switch to the correct branch and merge your changes again.

### Example 3: The Accidental Overwrite

Finally, another common Git Gaffe is accidentally overwriting someone else's changes without realizing it. This can happen when developers forget to pull the latest changes before pushing their own code.

```bash
$ git push origin master
To
    ! [rejected]        master -> master (fetch first)
error: failed to push some refs to '
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

### Example 4: The Hilarious Comment

Git Gaffes can also include hilarious code comments that were meant to be temporary or sarcastic, but were accidentally pushed to the repository. These comments can be embarrassing for developers, but they can also provide a good laugh.

```javascript
function divide(a, b) {
  // Because who needs error handling? :D
  return a / b;
}
```

The best way to avoid accidentally pushing a hilarious comment to your repository is to be mindful of the content of your code comments and commit messages. Remember that these comments are part of the public record and can be seen by anyone who has access to your repository.

If you have already pushed a hilarious comment to your repository, the best course of action is to remove it from the repository history using the `git rebase` command. This will allow you to remove the commit that contains the comment and rewrite the repository history.

This will open an editor window where you can select which commits you want to keep. In this case, you can remove the second commit by changing `pick` to `drop`:

```bash
$ git rebase -i HEAD~2
pick 3b0e5c1 Merge branch 'feature-branch'
drop 3b0e5c1 Add divide function
```

Once you have removed the commit, you will need to force push the updated history to the remote repository:

```bash
$ git push origin master --force
```

### Conclusion
Git Gaffes can be embarrassing for developers, but they can also provide an opportunity to learn from mistakes and improve Git skills. Remember to always double-check before making changes and use Git's
