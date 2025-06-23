# git-scripts

Useful custom scripts for git in the github and/or jira ecosystem.

## Installation

- Clone the repository and add the scripts to your PATH.
- Download individual scripts and add them to your PATH.

## Usage

Generally scripts outputs to the stdout commands that can be piped to a bash
shell. You can use editors (i.e. `vipe` command) for intermediate steps to
modify the commands. You should run git scripts in the root of your git
repository. You should force-with-lease push all changes to the PRs: scripts
are calculating range-diffs.

Example usage:

```bash
$ cd /path/to/repository
$ git ghj-print-pr-create | vipe | bash
```

### GitHub PRs + Jira Issues

Scripts used for GitHub and Jira: `git-ghj-*`. Scripts use GitHub CLI
(`gh`) and Jira CLI (`jira-cli`) to create/modify pull requests and issues.

There should be a Jira issue, eg `JIRA-123`. You should name branches with
`jira-123-` prefix. In the commit body you should reference the Jira issue
`JIRA-123`. Default remote is `origin`. The number of commits per patch is
calculated automatically based on branch names and jira tags in the commit
description body.

#### Creating a pull request

You should create a branch with the name `jira-123-branch-name` for the patch
and push it to the repo as `origin/jira-123-branch-name`.

```bash
$ git gh-print-pr-create | vipe | bash
```

#### Syncing a pull request

After rebasing locally branch `jira-123-branch-name` you shouldn't push it
manually. Instead run the script:

```bash
$ git gh-print-pr-sync | vipe | bash
```

The script will push force-with-lease the branch, calculate a range-diff,
add a comment to the PR with changelog (you should modify it in an editor)
update the pull request description (if this is single-commit patch).

#### Syncing an issue

You should add a comment to the Jira issue with the current list of PRs for
this issue:

```bash
$ git gh-print-issue-sync | vipe | bash
```

### GitHub PRs + GitHub Issues

Scripts used for GitHub and Jira: `git-gh-*`.

