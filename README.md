# PR TaskList Completed Checker Action
A GitHub action that checks if all tasks are completed in the pull requests.

## Usage

### Create a workflow
Put this file in the `.github/workflows/pr_tasklist_checker.yaml`

```yml
name: 'PR TaskList Completed Checker'
on: 
  pull_request:
    types: [edited, opened, synchronize, reopened]
  merge_group:
    types: [checks_requested] 

jobs:
  task-check:
    runs-on: ubuntu-latest
    steps:
      - uses: venkatsarvesh/pr-tasks-completed-action@v2.0.0
        with:
          repo-token: "${{ secrets.GITHUB_TOKEN }}"
```
Ensure that Github Actions are enabled in your repo:

![Enabling Github Actions](https://github.com/breakawaydata/pr-tasks-completed-action/assets/84781/06675403-9bb2-497a-84cb-bd6a1208ffed)

After you commit and merge, ensure the workflow is setup to block merging going forward. Under branch protections:

![Example Branch Protection Setup to block merging](https://github.com/breakawaydata/pr-tasks-completed-action/assets/84781/13478986-704e-4cad-a036-61b9b178a58a)


### Check whether tasks are completed
Add a pull request template to your repository (`.github/PULL_REQUEST_TEMPLATE.md`). See the example in this repo for a good template to use.

For example: 
```markdown
## Checklist
- [ ] Completed code review
- [ ] Ran unit tests
- [ ] Completed e2e tests
```

Create a pull request that contained tasks list to your repository. This will start a workflow automatically to check whether tasks are completed.

Every update on a pull request will start a new workflow automatically to check pending tasks.

All tasks completed:
![All tasks completed](images/success.png)

Some tasks are still pending:

![Some tasks are still pending](images/failure.png)

You can check a list of uncompleted tasks at the Actions page on clicking Details.
![List of pending tasks](images/pending_tasks.png)


## :memo: Licence
MIT
