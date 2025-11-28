# Git Flow Best Practice

```mermaid
%%{init: { 'logLevel': 'debug', 'theme': 'base', 'gitGraph': {'showBranches': true}} }%%
gitGraph
  commit
  branch develop
  checkout develop
  branch release/1.0.0
  checkout main
  branch feat/user1-task1-detail
  checkout main
  branch feat/user2-task2-detail
  commit
  commit
  checkout feat/user1-task1-detail
  commit
  commit
  checkout develop
  merge feat/user1-task1-detail tag: "Squash & Merge"
  checkout feat/user2-task2-detail
  commit
  checkout release/1.0.0
  merge develop tag: "Merge & CI/CD"
  checkout develop
  merge feat/user2-task2-detail tag: "Squash & Merge"
  checkout release/1.0.0
  merge develop tag: "Merge & CI/CD"
  checkout main
  merge release/1.0.0 tag: "Squash & Merge & CI/CD"
  checkout develop
  merge release/1.0.0 tag: "Merge"
  checkout main
  branch fix/user1-task1-detail
  checkout fix/user1-task1-detail
  commit tag: "fix: bug"
  checkout main
  merge fix/user1-task1-detail tag: "Squash & Merge & CI/CD"
  checkout develop
  merge fix/user1-task1-detail tag: "Merge"
  branch release/1.1.0
  branch feat/user1-task3-detail
  commit
  checkout develop
  merge feat/user1-task3-detail tag: "Squash & Merge"
  checkout release/1.1.0
  merge develop tag: "Merge & CI/CD"
```

From the git graph above, we can well-managed the branches with different purpose.

- [Release branch](#release-branch)
- [Feature branches](#feature-branches)
- [Hotfix branch](#hotfix-branch)

### Release branch

> Example: `release/x.y.z`

This branch is made for the upcoming production release. It is best branch to run the CI/CD for `staging` environment so that developers & testers can verify the reliability of the new release before deploy to `production` environment.

---

### Feature branches

> Example: `feat/userX-task-description`

Each branch gets a unique identifier combining the developer's name, task ID, and a critical description of the task. Get ready for streamlined collaboration and instant context. Embrace the power of clear branch names today!

---

### Hotfix branch

> Example: `fix/userX-bug-description`

By right all the bugs should be detected and fixed in `staging` environment so this branch should NOT exist but somehow Morphy's Law still works. Branch out from `main` and fix it ASAP, then open PR for `main` for testing in `staging` environment again before roll out to `production` environment. After squash merged into `main`, this shoud be merged with `--no-ff` into `develop`.
