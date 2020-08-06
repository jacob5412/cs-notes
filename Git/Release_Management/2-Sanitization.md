# Santiziation

## Rebasing vs Merging

1. Combine smaller to larger commits or vice versa - whichever is logically easier to understand. Alter the commit message.
2. Make sure your hotfix, feature or bugfix branch is based on the latest commit from the master.
3. Never rebase a public branch - master, deployment or staging

## Squashing Commits

1. Squash commits into a single commit whenever necessary. E.g. removed .DS_Store, removed .ipynb_checkpoints should be one commit.

## References

1. [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)