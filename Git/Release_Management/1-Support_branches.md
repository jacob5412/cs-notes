# Supporting Branches - Cheatsheet

Next to the main branches `master` and `develop`, our development model uses a variety of supporting branches to aid parallel development between team members, ease tracking of features, prepare for production releases and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a **limited life time**, since they will be removed eventually.

## Feature Branch

Feature branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release

### Creating a feature branch

When starting work on a new feature, branch off from the `develop` branch.

```bash
$ git checkout -b myfeature develop
Switched to a new branch "myfeature"
```

### Incorporating a finished feature on develop

Finished features may be merged into the `develop` branch to definitely add them to the upcoming release:

```bash
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff myfeature
Updating ea1b82a..05e9557
(Summary of changes)
$ git branch -d myfeature
Deleted branch myfeature (was 05e9557).
$ git push origin develop
```

## Release Branch

Release branches support preparation of a new production release.

### Creating a release branch

Say version 1.1.5 is the current production release and we have a big release coming up. The state of develop is ready for the “next release” and we have decided that this will become version 1.2 (rather than 1.1.6 or 2.0). So we branch off and give the release branch a name reflecting the new version number:

```bash
$ git checkout -b release-1.2 develop
Switched to a new branch "release-1.2"
$ ./bump-version.sh 1.2
Files modified successfully, version bumped to 1.2.
$ git commit -a -m "Bumped version number to 1.2"
[release-1.2 74d9424] Bumped version number to 1.2
1 files changed, 1 insertions(+), 1 deletions(-)
```

Here, bump-version.sh is a fictional shell script that changes some files in the working copy to reflect the new version.

Adding large new features here is strictly prohibited. They must be merged into develop, and therefore, wait for the next big release.

### Finishing a release branch

1. The release branch is merged into `master` (since every commit on master is a new release by *definition*).
2. That commit on `master` must be tagged for easy future reference to this historical version.

```bash
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2
```

3. Now we need to keep those changes in the `develop` branch.

```bash
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
```

4. Remove the `release` branch

```bash
$ git branch -d release-1.2
Deleted branch release-1.2 (was ff452fe).
```

Thereby, ending the lifetime of the `release` branch.

## Hotfix Branch

Hotfix branches are very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned. The essence is that work of team members (on the `develop` branch) can continue, while another person is preparing a quick production fix.

### Creating the hotfix branch

Say version 1.2 is the current production release running live and causing troubles due to a severe bug. But changes on `develop` are yet unstable. We may then branch off a `hotfix` branch and start fixing the problem:

```bash
$ git checkout -b hotfix-1.2.1 master
Switched to a new branch "hotfix-1.2.1"
$ ./bump-version.sh 1.2.1
Files modified successfully, version bumped to 1.2.1.
$ git commit -a -m "Bumped version number to 1.2.1"
[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
1 files changed, 1 insertions(+), 1 deletions(-)
```

Then, fix the bug and commit the fix in one or more separate commits.

```bash
$ git commit -m "Fixed severe production problem"
[hotfix-1.2.1 abbe5d6] Fixed severe production problem
5 files changed, 32 insertions(+), 17 deletions(-)
```

### Finishing a hotfix branch

When finished, the bugfix needs to be merged back into master, but also needs to be merged back into `develop`, in order to safeguard that the bugfix is included in the next release as well. Similar to `release` branches.

```bash
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2.1
```

Now, including bugfix in `develop`:

```bash
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
```

The one exception to the rule here is that, **when a release branch currently exists, the hotfix changes need to be merged into that release branch, instead of develop**.

Finally, remove the temporary hotfix branch:

```bash
$ git branch -d hotfix-1.2.1
Deleted branch hotfix-1.2.1 (was abbe5d6).
```

## Summary

|                           | Feature/Bugfix           | Release                | Hotfix                 |
| ------------------------- | :----------------------: | :--------------------: | :--------------------: |
| may branch off from       | `develop`                | `develop`              | `master`               |
| must merge back into      | `develop`                | `develop` and `master` | `develop` and `master` |
| branch naming conventions | *feature-\**/*bugfix-\** | *release-\**           | *hotfix-\**            |

## Git Branching Model

<object data="https://nvie.com/files/Git-branching-model.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="https://nvie.com/files/Git-branching-model.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="https://nvie.com/files/Git-branching-model.pdf">Download PDF</a>.</p>
    </embed>
</object>

## References

1. [A successful git branching model](http://nvie.com/posts/a-successful-git-branching-model/)