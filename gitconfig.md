# Example gitconfig file - The beginning of a beautiful relationship

## What is this crap?

The point of this file is to keep local configurations for Git as well as aliases.

Every time one enters/runs a `git config <something good>` command, an entry is added to the `gitconfig` file.

Example: `git config --global user.name "Ron Burgundy"` => This would add the `name = Ron Burgundy` entry below.


## An example file

```
[user]
  name = Ron Burgundy
  email = ron@tegra.is
[core]
  editor = code --wait
  autocrlf = false
  safecrlf = true
[alias]
  br = branch
  ci = commit
  co = checkout
  pl = pull
  st = status
  sw = switch
  please = push --force-with-lease
  plorb = pull --no-rebase
  publish = push -u origin HEAD
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  log1 = log --oneline --decorate
  undo1cm = reset --soft HEAD~1
  type = cat-file -t
  dump = cat-file -p
[rebase]
  autosquash = true
[pull]
	rebase = true
```

### [user] section

The info in this section is essential, for example in the Author line for commits:

```
commit fe83ba0bb9c7e97fbbb47e8798e8ca4c7dc75395
Author: Ron Burgundy <ron@tegra.is>
Date:   Thu Dec 24 18:07:44 2021 +0100

    feat: Some very informing text
```

### [core] section

This section contains core configurations e.g. text handling.

In the example above, we have 3 lines:

- `editor = code --wait` tells Git that we wish to use Visual Studio Code (`code`) as our text editor for Git.
  - Note that
  - The `--wait` flag is used so that the command line will wait for a certain process to be finished (by/in the editor) before work can be resumed.
- Regarding `autocrlf` and `safecrlf`... Yamahama! This tends to be an issue when worlds collied, e.g. same files are edited on DOS (Windows) and *nix-based OS's. By setting `autocrlf` to false, line-breaks (or eol's, whatever you want to call them) will not be automatically changed.
- This topic is not very inspiring but in case anyone is interested => [this](https://www.aleksandrhovhannisyan.com/blog/crlf-vs-lf-normalizing-line-endings-in-git/).

### [alias] section

This is the most personalized section since these are simply aliases for valid Git commands. The example above contains those that a certain jolly dude would consider essential or at least very convenient.

One should feel encouraged to change alias names to suit one's needs/preferences. Should people fine themselves using a certain Git command often, they should consider creating an alias for said command, especially if it's a big one!

### [rebase] section
The `autosquash = true` setting is included to aid when [using `fixup` commits](https://thoughtbot.com/blog/autosquashing-git-commits).

```
# It eliminates the need for the --autosquash flag | Great savings ;)
## From:
git rebase --interactive --autosquash main
## To:
git rebase --interactive main
```

### [pull] section

The main reason for the `rebase = true` setting is so that every time one pulls, a merge-commit will not be created (may be required unless we rebase first). We could simply add a `--rebase` flag to the alias `pl = pull --rebase` and that would work just fine (as long as one uses the `pl` alias instead of `pull`). The problem is often with these pesky GUI tools for Git, they often don't care about a nice clean Git history. Most/some of them do however respect the `gitconfig` file.