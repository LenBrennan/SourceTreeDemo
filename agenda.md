# Change these defaults (Tools &rarr; Options)

### General

- Language: *Automatic &rarr; English* (spooky denglish; obfuscates under-the-hood commands)
- Project folder: *blank &rarr; $GITROOT* (every file dialog will open this by default)
- Always display full console output: *false &rarr; true*	(tells you whats's going on under the hood, can be closed by pressing enter)
- Use fixed-width font for commit messages: *false &rarr; true*
- Display a column guide in commit messages at: *false &rarr; true; 72* (keep it short and simple; [post on subject](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html))
- After commiting, stay in commit dialog if there are still pending changes: *false &rarr; true* (helps when committing atomically)


### Git
- Push branches: *matching &rarr; simple* (not all tracked branches are checked when pushing; this mode will be the default in git 2.0 )

###### LARGELY OPIONION-BASED
- Use rebase instead of merge by default for tracked branches: *false &rarr; true*
- Do not fast-forward when merging, always create commit: *false &rarr; true*



# Nice to know
- The commit hash is a clickable link. Use it in a commit message when you reference another commit.
- The current branch is printed in bold. (cf. `git branch -a`)
- Branches are grouped in folders when their names contain a slash. (e.g. *release/1.4.1*)
- You can stage segments or specific lines instead of entire files in the diff view. Beware that this might not work when the file's encoding and git encoding differ.
- In the graph view the current branch is the leftmost.



# No-Nos
- Tools &rarr; Settings &rarr; Push to default/origin when committing (git != SVN)
- Blindly pulling with unpushed commits. This will result in unwanted *"merge branch XXX from https://origin into XXX"* commits.
However pulling is no problem with an uncommitted working copy.



# Scenarios

> I made some commits and want to push them as one single commit

1. Make sure you have not pushed your commits yet
2. Right click the commit you want to push
3. *Reset current branch to this commit*
4. Select soft mode (all changes are left in your working copy AND the index is left intact)
5. Make a new commit containing all of your changes

&nbsp;

&nbsp;


> I made some commits but I'd like to only push the first two

##### SourceTree way
1. Create a new branch out of your current state (e.g. *temp/I_WANT_YOU_BACK_FOR_GOOD*) but do not check it out
2. In your original branch right click the last commit you want to push
3. *Reset current branch to this commit*
4. Select hard mode (all changes are deleted! Make sure you created the backup branch in step 1)
5. Push your commits
6. Right click the HEAD commit of your backup branch
7. Select merge (don't use *create a new commit even if fast-forward is possible*)
8. Delete the temp branch


##### Git way
Assuming you have 5 commits and want to push the first two
`git push origin <localBranchName>~3:<remoteBranchName>`


&nbsp;

&nbsp;


> I've been working on the wrong branch

Assuming you have not pushed your commits:

##### If you started from the right branch (e.g. starting a feature but committed straight into develop)
1. Create a new branch out of your current state (but don't check it out)
2. Right click the last commit in the current branch before you started your work
3. *Reset current branch to this commit*
4. Select hard mode (all changes are deleted! Make sure you created the branch in step 1)
5. Switch to your newly created branch


##### If you started from the wrong branch (e.g. starting a hotfix but from a feature branch instead of master)
1. Switch to the correct starting branch
2. Create a new branch from there and check it out
3. Cherry pick every commit that from your wrong branch starting with the oldest (set log view to show all branches and
right click the commit to select *cherry pick*)
4. Reset the wrong branch to a state before your commits using hard mode (check if the cherry pick worked out as
planned before)

&nbsp;

&nbsp;


> I'm not sure if a certain commit is included in the current state


##### SourceTree way
1. Copy the commit's hash
2. Set log view to show current branch only
3. Use *Jump to: &rarr; commit &rarr;* paste hash and press enter
4. If the commit is not found/ listed, it's not in the current branch

##### Git way
1. Copy the commit's hash
2. Open git shell and type `git branch --contains <hash>`
3. All branches containing the commit will be listed; the current branch is highlighted

&nbsp;

&nbsp;


> My local changes are rubbish, I want to get the current state from origin.

1. Make sure you're on the right branch.
2. Fetch
3. Right click the latest commit on origin.
4. *Reset current branch to this commit*
5. Select mode hard

&nbsp;

&nbsp;


> I prematurely pushed commits and want to undo the commits on origin.

##### SourceTree way
Do the following with every falsely pushed commit, starting with the *newest*:
1. Right click the commit
2. *Create reverse commit*

##### Git way
1. `git reverse HEAD~0`
2. `git reverse HEAD~2`
3. `git reverse HEAD~4`
4. ... (add 2 for as many commits as you have to 'undo')

&nbsp;

Push all reverse commits afterwards.

&nbsp;

&nbsp;



# Custom actions
Are a way of integrating your own git scripts in SourceTree. See https://github.com/FatherStack/SourceTree-Custom-Actions
