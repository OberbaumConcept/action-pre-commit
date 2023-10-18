# action-pre-commit

a GitHub action to run [pre-commit](https://pre-commit.com)

Fork of [pre-commit/action](https://github.com/pre-commit/action), added support to skip hooks.


# using this action

To use this action, make a file `.github/workflows/pre-commit.yml`.  Here's a
template to get started:

```yaml
name: pre-commit

on:
  pull_request:
  push:
    branches: [main]

jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-python@v3
    - uses: OberbaumConcept/action-pre-commit@1.0.0
```

This does a few things:

- clones the code
- installs python
- sets up the `pre-commit` cache
- runs pre-commit

## Using this action with custom invocations

By default, this action runs all the hooks against all the files.  `extra_args`
lets users specify a single hook id and/or options to pass to `pre-commit run`.

Here's a sample step configuration that only runs the `flake8` hook against all
the files (use the template above except for the `pre-commit` action):

```yaml
    - uses: OberbaumConcept/action-pre-commit@1.0.0
      with:
        extra_args: flake8 --all-files
```

## Using this action skipping some hooks

By default, this action runs all the hooks against all the files.  `skip_hooks`
lets users specify hooks to skip when running `pre-commit run`. This is a comma
separated list of hook ids to skip.

Here's a sample step configuration that skips the hook `no-commit-to-branch`:

```yaml
    - uses: OberbaumConcept/action-pre-commit@1.0.0
      with:
        skip_hooks: no-commit-to-branch
```
