# Git Hooks Repo Example

This repo contains an example of git hooks being contained within the repo. While it's not for all projects,
it can be useful for closed environments of developers to run quick tests before committing.


## How it works

Everything related to the git hooks lives in the git-misc directory. The most important part of this dir is the
updateHooks.sh script. Anytime this script is run, it silently copies all the files in `$repoRoot/git-misc/git-hooks/*` to
`$repoRoot/.git/hooks/`, also removing all existing hooks.


The real magic comes from running the updateHooks.sh in every hook. This effectively means that any real action on the 
repo will cause the hooks to be updated.

All that is required is running `enableGitHooks.sh` once, and from there on, hooks will be synced with the repo.


## User Specific hooks

You can also create a directory called `$repoRoot/git-misc/git-hooks-nosync/` if you want to create hooks which are not synced
to the rest of the users. Any hooks in this directory are copied on top of the synced hooks, after the synced hooks are applied.
This directory is in `.gitignore`, so they will never be synced. This nosync directory allows you to issue a manual override of 
synced hooks, since all the files in the `.git/hooks` directory are overwritten frequently.



