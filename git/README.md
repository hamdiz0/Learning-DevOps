# `GIT` 

- [USING GIT ON A LOCAL MACHINE](#using-git-on-a-local-machine)
   - [show version](#show-version)
   - [set up name and email / repo](#set-up-name-and-email--repo)
   - [set up a text default editor](#set-up-a-text-default-editor)
   - [initialize current folder as a git repo](#initialize-current-folder-as-a-git-repo)
   - [check config](#check-config)
   - [clone a repo](#clone-a-repo)
   - [show repo status](#show-repo-status)
   - [add changes to the staging/tracking area](#add-changes-to-the-stagingtracking-area)
   - [restore and discard changes](#restore-and-discard-changes)
   - [commit changes](#commit-changes)
   - [commit history](#commit-history)
   - [show difference or changes to what git already knows](#show-difference-or-changes-to-what-git-already-knows)
   - [restore history or previous state](#restore-history-or-previous-state)
   - [ignore files](#ignore-files)
   - [track empty dirs](#track-empty-dirs)
   - [aliases](#aliases)
   - [update or change a commit](#update-or-change-a-commit)
- [USING GIT REMOTELY](#using-git-remotely)
   - [local/remote communication](#localremote-communication)
   - [set up|remove remote repo](#setupremove-remote-repo)
   - [ssh](#ssh)
   - [push](#push)
   - [pull](#pull)
   - [conflicts](#conflicts)
   - [set up personal access token PAT](#set-up-personal-access-token-pat)
- [BRANCHES](#branches)
   - [create and switch between branches](#create-and-switch-between-branches)
   - [merging](#merging)
   - [rebase](#rebase)
   - [squashing commits](#squashing-commits)
   - [pull requests & merging branches in GitHub UI](#pull-requests--merging-branches-in-github-ui)
   - [update the log](#update-the-log)
   - [control HEAD pointer position](#control-head-pointer-position)
- [GIT WORKFLOWS WORKING WITH COLLABORATORS](#git-workflows-working-with-collaborators)
   - [adding collaborators](#adding-collaborators)
   - [adding branch protection rules](#adding-branch-protection-rules)
   - [git flow](#git-flow)
   - [forking](#forking)

#                                        [`USING GIT ON A LOCAL MACHINE`]

## `show version` :

        - git --version

## `set up name and email / repo` :

        - git config --global user.name "name"
        - git config --global user.email "email"

## `set up a text default editor `:

        - git config --global core.editor "nano -w" (nano)
        - git config --global core.editor "code --wait" (vscode)

## `initialize current folder as a git repo`  :

        - git init

## `check config` :

        - git config --list

## `clone a repo` :

        - git clone "url"

## `show repo status` :

        - git status

## `add changes to the staging/tracking area` :

        - git add "file"
        - git add . (add evrything in the current path)

## `restore and discard changes` :

        - git restore "file"

## `commit changes` :

        - git commit (opens text editor to write a msg)
        - git commit -m "message" (write msg directly)
        - git commit -am "message" (add all changes in the current dir and commit)

## `commit history` :

        - git log ("HEAD => main" present on the current last commit)
        - git log --oneline

## `show difference or changes to what git already knows` :

        - git diff (compare current uncommitted state with last known state)
        - git diff --staged (see differences after adding changes to the staging area)
        - git diff HEAD~2 (compare HEAD "current state" with relative commit number ago)
        - git diff "hash" (see difference between current state and previous commits using hash identifier)

## `restore history or previous state` :

        - git restore "file" (restore current state to the last known state)
        - git restore --source "hash"|HEAD~2 "file" (restre to a particular state)
        - git checkout "hash" "file" ("detatched head state" if file is not specified type git switch - or git ckeckout main to undo changes)

## `ignore files` :

        * specifie dirs/files/patterns in ".gitignore" to ignore it
        * ".gitignore" file must be committed

## `track empty dirs` :

        * add a ".gitkeep" inside an empty dir to keep track of it
        * ".gitkeep" file is just a convention not a special file

## `alaises` :

        - git config --global alias."alias" "command"

## `update or change a commit` :

        - git commit --amend -m "message" (change last commit message)

#                                        [`USING GIT REMOTLY`]

## `local/remote communication` :

        * it's better to initialize the repo on the remote web service first
        * clone clones a remote web repo on a local machine

## `set up|remove remote repo` :

        - git remote -v (show current remote connections fetch/push)
        - git remote add "remote name(origin)" "repo url from web service"
        - git remote rm "remote name(origin)" (removes remote connection)
        - git rename "old remote name" "new name"

## `ssh` :

        - ssh-keygen (generates an ssh key "in bash")
        * github => account settings => ssh & gpg keys
        * copy the public key under "~/.ssh(linux)"|"C:/users/user/.ssh(win)" to key tab under ssh & gpg section
        * set up remote connection using ssh url (git remote add "name" "url")
        * make sure to remove the current remote connection "https" (git remote rm "name")

## `push` :

        - push : local => remote
        - git push "remote(where to push to)" "local(from what bransh)"
        - git push -f(force) "remote(where to push to)" "local(from what bransh)"
        - git push --force-with-lease "remote(where to push to)" "local(from what bransh)" (more mindfull of collaborators)

## `pull` :

        - pull : reote => local
        - git pull "remote(where to pull from)" "local(to what bransh)"

## `conflicts` :

        * if remote and local both committed diffrent changes
        * pushing changes (from local) requiers pulling from remote first
        - git merge --abort (returns to the state before pulling from remote)


## `set up personal access token PAT` :

        - git web service (github) => account settings => developer settings => PAT
        - printf "host=github.com\nprotocol=https\n" | git credential fill (chow pat conf)
        - printf "host=github.com\nprotocol=https\n" | git credential reject (remove pat conf)

#                                        [`BRANCHES`]

* it's better to work in feature branches than merge changes into the main branchs

## `create and switch between branches` :

	* it's better to pull from main (remote) before creating a branch
        - git branch "branch" (create a new branch)
        - git branch -a (list all branchs)
        - git branch -d "branch" (delete a branch "-D force delete")
        - git switch "branch" (switch to a branch) ,git ckeckout "branch name"
        - git switch -c "branch" (create and switch to a branch) ,git ckeckout -b "branch name"
        * moving between branches requiers commiting or stashing changes (more than one commit)
        - git stash (teporarly save changes or a commit allowing branch switching)
        - git stash list (show current stashed commits {"index"})
        - git stash apply "index" (apply a stashed commit)
        - git stash clear (clear stashes)

## `merging` :

        * merge a branch changes to the main branch or another branch
        - in the a branch "main" : git merge "the branch with the changes"
        - O => O *\=> O => O  /*=> O  (O:main branch)
                   \=>O1=> O1/

## `rebase` :

        - git rebase "branch" incorporate changes from "branch(main)" into current "branch(feature)"
        - git rebase --abort (abort rebase)
        - git rebase --continue : icorporate desired changes (git add .) than run this command in case of conflicts
        - O => O *\=> O1=> O1   =\   O => O => O1=> O1 *\
                   \=>O2=> O2   =/                       \*=> O2=> O2
        * rewrite the history of a commit
        * git status helps working with rebase
        * merge into main branch after incorporating changes and fixing conflicts in the feature branch
        * rebase is used when the "main branch" commited changes that are not avaible for a "feature branch" to rewrite it's history and fix conflicts to make it ready for merging whith main

## `squaching commits` :

        - git rebase -i "hash(+"^":one hash before)"|HEAD~"number"
        * set "s" in "pick" before the commit to squach it with the previous commit

## `pull requests & merging branches in GitHub ui` :

        * under code tab select desiered branch (drop down menu) than click on "contribute" to create a pull request
        * it's possible to update the branch in the remote locally (git push "remote" "branch")

## `update the log` :

        - git fetch (update git log without changing files)
        - git fetch --prune (update and remove deleted branches in the git log)
	- git fetch --prune --all (update git log from all avaible remotes)

## `control HEAD pointer position` :

        - git reset --hard "hash"|"branch(origin/main)" (move HEAD pointer to a specific commit)

#                                        [`GIT WORKFLOWS WORKING WITH COLLABORATORS`]

## `adding collaborators ` :

	* repo settings => cloborators => add people
	* resync history or pull the latest changes before creating a branch 
	* feature branches (pull requests) won't show conflicts until one of them is merged first
	
## `adding branch protection rules` :

	* repo settings => branches => add rule (specifie branch name and select desired rules)
	* add rules to make it that not anybody can push their changes to a certain branch (main)
	* add pull requests rules so that pull requests require reviewing (certain number of reviews) and approuval before merging	
	* set bypass exception rules to get certain preveliges as the owner

## `git flow` :

	* setting seperate branches for production(main) and development(dev) wich can contain multiple sub-branches(feature)
	* sub-branches commit their changes against the "dev" branch (merged against dev) 
	* when these changes are tested and approuved their are ready to merge with "main"
	- (main) O => O => O *\ ===============================================> /*=> O	
			       \ (dev) O => O => O *\ =================> /*=> O / 		
			      			     \ (feature) O => O /	

## `forking` :

	* forking workflow is commonly used in open source projects
	* copy the original remote repo into youre account
	* the remote copy is called origin
	* the original copy is called "upstream"
	* it's better to follow the branching workflow used by the original copy (upstream) 
	- git remote add "upstream" "url" (adding the original copy remote (upstream) to stay up to date)
	






