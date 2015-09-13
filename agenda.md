# Change these defaults (Tools ? Options)

### General

- `Language: Automatic ? English` (spooky denglish; obfuscates under-the-hood commands)
- `Project folder: blank ? $GITROOT` (every file dialog will open this by default)
- `Always display full console output: false ? true`	(tells you whats's going on under the hood, can be closed by pressing enter)
- `Use fixed-width font for commit messages: false ? true`
- `Display a column guide in commit messages at: false ? true; 72` (keep it short and simple; [post on subject](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html))
- `After commiting, stay in commit dialog if there are still pending changes: false ? true` (helps when committing atomically)


### Git
- `Push branches: matching ? simple` (not all tracked branches are checked when pushing; this mode will be the default in git 2.0 )

###### LARGELY OPIONION-BASED
- `Use rebase instead of merge by default for tracked branches: false ? true`
- `Do not fast-forward when merging, always create commit: false ? true`



# Nice to know
- The commit short hash is a clickable link. Use it in a commit message when you reference another commit.
- The current branch is printed in bold. (cf. `git branch -a`)
- Branches are grouped in folders when their names contain a slash. (e.g. *release/1.4.1*)
- You can stage segments or specific lines instead of entire files in the diff view.
- In the graph view the current branch is the leftmost.



# No-Nos
- Tools ? Settings ? Push to default/origin when committing (git != SVN)
- Blindly pulling with unpushed commits. This will result in unwanted *"merge branch origin/XXX into XXX"* commits.
However pulling is no problem with an uncommitted working copy.



# Scenarios

> I made some commits and want to push them as one single commit


> I've been working on the wrong branch


> I'm not sure if a certain commit is included in the current state

##### SourceTree way
1. Copy the commit's hash
2. Set log view to show current branch only
3. Use Jump to: ? commit ? paste hash and press enter
4. If the commit is not found/ listed, it's not in the current branch

##### Git way
1. Copy the commit's hash
2. Open git shell and type `git branch --contains <hash>`
3. All branches containing the commit will be listed; the current branch is highlighted


> My local changes are rubbish, I want to get the current state from origin.
1. Make sure you're on the right branch.
2. Fetch
3. Right click the latest commit on origin.
4. `Reset current branch to this commit`
5. Select mode hard


> I prematurely pushed commits and want to undo the commits on origin.



# Custom actions
Are a way of integrating your own git scripts in SourceTree. See https://github.com/FatherStack/SourceTree-Custom-Actions