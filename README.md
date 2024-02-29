# What does it do?

This action retrieves a list of people who contributed to the repo and updates the `CONTRIBUTORS` text file in the root of the project.
The commit is done by `github-actions[bot] <github-actions[bot]@users.noreply.github.com>`.

The list of contributors will look like this:

```text
Contributor A <email-of-a@example.com>
Contributor B <email-of-b@example.com>
```

The list will be sorted alphabetically in a case-insensitive manner. Users with `[bot]` in their username or email will be omitted.

# How to use it?

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
      - name: update
        uses: tessus/update-contributors-list@v1
```
