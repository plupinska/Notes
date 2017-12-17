# Git Notes

## Part I: General workflow stuff

#### Saving aliases to git config:
Git config `—global alias.name ‘command’`

#### STASHING
`git stash -u`

(because by default it doesn’t pick up untracked files)

#### DECORATED GIT LOG
git log --`oneline --decorate --graph --all -30`
* oneline gives you abbreviated commit hash and message
* decorate color codes by branch local and remote history
* graph all gives complete branch history with lines

#### CUSTOM LOG FORMAT
`git log --pretty=format:'%h - %an [%ar] %s'`

%h abbreviated commit hash
%an author name
%ar relative date
%s commit subject

##### COLORING THIS
n addition, we can spruce this up by adding a little color. Colors are specified with %C(<color-name>), with %C(reset) resetting the color. In the following, we color the commit hash yellow and the date green:

`git log --pretty=format:'%C(yellow)%h%C(reset) - %an [%C(green)%ar%C(reset)] %s'`

#### SEARCHING THE LOGS BY COMMIT MESSAGE
`git log —grep -E -i ’some(thing)’`

-E use extended regex
-i case insensitive

#### SEARCHING THE LOGS BY CODE CHANGE
`git log -S this_method_i_worked_on`

#### FILE SPECIFIC GIT LOG
`git log —oneline —Gemfile`

#### GIT BLAME
`git blame Gemfile`

#### LOOKING AT THE DIFF OF A PARTICULAR COMMIT
`git show commit_hash`

## Part II: Undoing all of your mistakes 🙏🙏🙏🙏🙏🙏

#### AMENDING COMMITS
`git add file_i_forgot_to_add.rb`
`git commit --amend --no-edit`

This will take the currently-staged changes and incorporate them into the previous commit, reusing the existing commit message thanks to the --no-edit flag.

`git commit --amend` wll amend your last commit messages.

#### REVERTING BACK TO THE LAST COMMIT
`git checkout .`

your stuff will dissapear. dangerous.

#### WORKING IN THAT EDITOR
0 is exit code.
:cquit or :cq to quit vim


## Part III: Crafting your History

#### CHERRY PICKING
Have you made a commit on the wrong branch?

Let's save you made 2 commits on master. but they should be on branch doing_stuff.
You can specify a commit range from origin/master to master.
ie, check `git diff origin/master ..master`

checkout out your feature branch and run

`git cherry-pick origin/master ..master`

git will create a new commit for each in the range and output a summary of the new commits.

#### RESET HARD

Cherry picking won't destroy the commits on master. just c+p them onto your branch.
to destroy the ones on master,

`git checkout master` + `git reset --hard origin/master`


#### REBASING

When we rebase, we do it from the context of our feature branch, and we specify the target branch we want to to rebase onto.


`git rebase branch-you-r-rebasing-onto`


Interactive Rebase: `git rebase -i master`
