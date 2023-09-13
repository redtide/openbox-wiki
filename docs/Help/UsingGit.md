# Using Git

## Quick instructions

The following command will create a directory called "`openbox`" and
download the source code into it (i.e., will create the local copy of
external repository):

```bash
git clone https://github.com/danakj/openbox.git
```

The following command will get the latest changes from external
repository and store them to the downloaded local repository:

```bash
git pull
```

Note however that this only does what you expect, if you haven't made
any changes. If you have, it will attempt to merge your changes, which
may or may not be what you want; see "[Local changes](#local-changes)" below.

## Branches

There are two main branches in the Openbox git repositories: "**work**"
and "**master**". The difference is that our "work" branches can have
testing stuff and be rebased (which means, git will get confused, if you
try to pull from them). Once we are pretty sure something will at least
not blow up, it will be put on the "master" branch and we try not to
rebase that unless really needed.

By default you will get the "master" branch, hence the name. If you want
the "work" branch, the first time you will need to run:

```bash
git checkout --track -b work origin/work
```

or if you have a recent git (somewhere in 1.6.x), you can just do:

```bash
git checkout -t origin/work
```

You can now switch between branches with `git checkout master` and
`git checkout work`.

If you want the very latest changes, first decide, if you want "master"
or "work". For "master" you can usually just run `git pull`, but if
you're on "work", you probably want to run something like:

```bash
git fetch ; git reset --hard origin/work
```

Note though that this will delete **all** local changes to checked out
files and also any commits you've made on the current branch. If you do
have commits, you can try `git pull --rebase`, but no guarantees. If
something goes wrong, anything you've committed is actually still
available, read the `git-reflog` man page for details. Uncommitted
changes will be gone after a reset `--hard` though.

## Local changes

Unlike CVS and Subversion, git lets you have local changes while still
tracking upstream development. In a nut shell, make your changes and
run:

```bash
git commit -a -m "informative message"
```

It's usually a good idea to keep your changes in a separate branch. You
can do this in a couple of ways. The easiest way is to run:

```bash
git checkout -b my-branch master
```

and then commit all your changes to that branch.

### Conflicting changes

If you hang on to your changes for a long time, it's likely that we will
make commits, that conflict with yours. There are two ways to deal with
this. You can either `git-merge` our branch and resolve the differences,
but the better way is to use `git-rebase`. Last command will take your
commits and apply them to the tip (the latest version) of the specified
branch, pausing after each commit that conflicts. This usually makes it
easier to resolve the conflicts and also gives a nicer history. Using
`git-rebase` is a bit complicated, so read the man page.

If you just want to test that your changes work with the latest version
of Openbox, you can merge "master" branch and then later use
`git reset --hard HEAD^` to revert the merge. However, I recommend first
doing a `git checkout -b my-temp`, since running `git reset` twice will
continue reverting real commits, so it's easy to mess up. If you're
doing all the temp merging on a separate branch you don't have to worry
about that.

## Contributing code

### GitHub workflow

If you'd like to use the GitHub workflow, then make a fork of the
Openbox git repo above via [GitHub](https://github.com), and send pull
requests from your branch with your code changes. GitHub has
[documentation](https://help.github.com), describing this process.

### BugZilla workflow

You've coded an exciting feature and want to send a diff? How to do it?
`git diff` you might guess, and while that will produce a diff you can
send. `git format-patch` is a bit nicer as it will automatically give
you a patch file per commit that you want to send, with the commit
message in each file.

In the simple case, where you just want to send off the top commit from
your repo, do:

```bash
git format-patch -1
```

If you have a bunch of patches and you have git 1.7 you can do:

```bash
git format-patch @{u}
```

and it will figure out the correct branch to consider "upstream" and
spit out a bunch of patch files. If you don't, you have to give the
range manually, but it will almost always be:

```bash
git format-patch origin/master
```

Once you have your patch(es), open a bug in the bugzilla as instructed
[here](../Contribute.md).

Another option is to set up your own public repo and simply tell us
where to pull your changes from. Look at the `git-daemon` man page for
details. This is not really preferred usually though, and you'll
probably need to be patient and hang around in the [IRC
channel](../Community/Portal.md) for a while.

## Low bandwidth option

If your internet connection is very slow (the full git repo is currently
around 8.5 MB) and you just want the very latest version without any
history, you can run:

```bash
git clone --depth 1 https://github.com/danakj/openbox.git
```

This will give you only the current and preceding commit from each
branch, but you can't do much more with your repo than compile the code.
Merging as described above will only work, if you use a depth high
enough to include the point, where the "backport" branch separated from
"master" branch. See the `git-clone` and `git-fetch` man pages for
further details.

You can also download a tarball of any revision via
[gitweb](http://git.openbox.org/?p=dana/openbox.git;a=summary). Click
"tree" next to a branch name at the bottom, then click "snapshot" at the
top of the new page.

## Alternate repos

Due to the distributed nature of git, you can choose to pull from
various upstream locations (see the `git-remote` man page for details on
how to use several remotes):

[git://git.openbox.org/dana/openbox](git://git.openbox.org/dana/openbox)<br />
[git://git.openbox.org/mikachu/openbox](git://git.openbox.org/mikachu/openbox)<br />
[git://git.mika.l3ib.org/openbox.git](git://git.mika.l3ib.org/openbox.git)<br />
[git://repo.or.cz/openbox.git](git://repo.or.cz/openbox.git)<br />
[git://github.com/Mikachu/openbox](git://github.com/Mikachu/openbox)<br />
[git://github.com/danakj/openbox](git://github.com/danakj/openbox)

The astute git user will notice, that there are some variations in
branches offered among these, for example dana has a "libs" branch that
separates out some common wm code in a library, and mikachu has a
"mikabox" branch which is just some crazy stuff.

## Further reading

On the [git home page](https://git-scm.com/) there are many great tutorials
and all the man pages are available for browsing as well.
