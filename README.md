# Git Push Force with Lease

`git` is a powerful and complex CLI that manages versions of your code. This lesson explores using the `git push --force-with-lease` and `git push --force`.

## The Manual

It is helpful to utilize [`git` documentation](https://git-scm.com/doc) often as you grow as a developer. Sometimes it is even easier to launch `git` documentation in your shell session. Let's do this right now for `git push`, using the `--help` option. You can pass the `--help` option to any `git` command for more information.

```
git push --help
```

Take a few minutes to read about some of the ways one can pass additional options and configuration to `git push`.

---

## Git Push Failures

Our normal workflow typically has us using `git push` with no issues. However, we will start to encounter new scenarios with `git` when we start working with more contributers. And there are times when simply using `git push` will not work. `git` informs us that it failed to push our changes with this blurb:

```
$ git push origin some-branch
To github.com:username/my_repo.git
 ! [rejected]        some-branch -> some-branch (non-fast-forward)
error: failed to push some refs to 'git@github.com:username/my_repo.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

The `hint:` above specifies why this has happened. `Updates were rejected because the tip of your current branch is behind its remote counterpart.`. There are two main reasons this may happen:

1. Another contributor has pushed a commit onto our branch and we have not synced our local copy by "pulling it down".
1. We have rewritten the history of one or more commits on our local copy and our commit hashes do not match up on Github.

Rewrite history? -- Do not worry about this now, we will talk more about it in lessons to come.

## Forcing Git Commits

To get our commits successfully `push`ed up to Github, we will need to specify a `force` option with the command. Enter `--force-with-lease`. If we have rewritten history for only our own commits, `--force-with-lease` will update Github with our new ones. Hooray! And happily, if `--force-with-lease` detects that there are untracked commits by another contributor on our branch, it will fail once again. This informs us that we need to `git pull` a fresh copy of the project and resolve any conflicts.

`--force-with-lease` is the best option to use here because it will save us from overwriting someone else's work. The less safe version for this command is simply `--force`, but we run the risk of messing up our project when we use it.

Here is `--force-with-lease` in action for our last failed `push`:

```
$ git push origin some-branch --force-with-lease
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 479 bytes | 479.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:powerhome/phrg-git-push-force-with-lease.git
 + dbe87f8...9c6180e some-branch -> some-branch (forced update)
```

Success!

## Still unclear?

Force pushing commits with `git` starts to make more sense when we encounter scenarios that require its use. Even after that, it still takes a good amount of experience to get comfortable using `--force-with-lease`. For now, know that forcing a commit is a option when you encounter a failed `git push`.

## Resources

- [`git` documentation](https://git-scm.com/doc)
- [`git push --force-with-lease` documentation](https://git-scm.com/docs/git-push#git-push---no-force-with-lease)
- [`git push --force` documentation](https://git-scm.com/docs/git-push#git-push---force)
- [--force considered harmful; understanding git's --force-with-lease](https://developer.atlassian.com/blog/2015/04/force-with-lease/)
