# What does it do?

This action retrieves a list of people who contributed to the repo and updates the `CONTRIBUTORS` text file in the root of the project.
It takes a possible `.mailmap` file into account.

The list of contributors will look like this:

```text
Contributor A <email-of-a@example.com>
Contributor B <email-of-b@example.com>
```

By default the list will be sorted by the numbers of commits, unless the number of contributors is greater than 30, in which case the list is sorted alphabetically in a case-insensitive manner.
The changes will be committed by `github-actions[bot] <github-actions[bot]@users.noreply.github.com>`.
Users with `[bot]` in their username or email will be omitted.

All these defaults can be overridden with optional inputs for the action.

# Inputs

All inputs are optional.

| Name                     | Description                                                                                                                         |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `sort-by`                | Sort contributors by: `name`, `commits`, `auto`<br>Default: `auto`                                                                  |
| `sort-by-auto-threshold` | If `sort-by` is set to `auto`, the list is sorted by name, when the number of contributors reaches this threshold.<br>Default: `30` |
| `commit-message`         | The commit message for updating the file.<br>Default: `chore: update CONTRIBUTORS`                                                  |
| `committer-name`         | The committer's name.<br>Default: `github-actions[bot]`                                                                             |
| `committer-email`        | The committer's email address.<br>Default: `github-actions[bot]@users.noreply.github.com`                                           |
| `exclude`                | A comma separated list of case-insensitive and literal patterns to exclude from the list.<br>Default: `[bot]`                       |

# Example workflow

```yaml
name: Update CONTRIBUTORS file
on:
  schedule:
    - cron: "0 0 1 * *"
  workflow_dispatch:
jobs:
  update_contributors:
    runs-on: ubuntu-latest
    steps:
      - name: Update Contributors
        uses: tessus/update-contributors-list@v3
```
