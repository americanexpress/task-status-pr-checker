# Github Actions

This repository contains actions used within American Express Github repositories.

## Task Status Pull Request Checker

This is triggered when a pull request is created. If the pull request has pending tasks. The pull request won't be merged and the status is updated on the pull request checks.

### How to enable this action

1. Create a[github workflow](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow) in your repository and add the below.

```yaml
on:
  pull_request:
    types: 
      - opened
      - edited
  pull_request_review_comment:
    types: 
      - created
      - deleted
      - edited
  issue_comment:
    types: 
      - created
      - deleted
      - edited
jobs:
  task_checker:
    runs-on: ubuntu-latest
    name: Check for tasks in pull requests
    steps:
    - name: Pull request task checker
      uses: americanexpress/actions/task-status-pr-checker@v1
      with:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

2. Pending tasks

![Pending task](./task-status-pr-checker/pending-task.png)

3. Completed tasks

![Completed tasks](./task-status-pr-checker/complete-task.png)
