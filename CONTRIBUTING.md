# Contribution Guidelines

# Installation

1. Clone the repository:
   ```shell
   git clone <repo_ssh_address>
   ```
1. Install uv using the instructions from the [official uv documentation](https://docs.astral.sh/uv/getting-started/installation/)
1. Switch to the project directory:
   ```shell
   cd <project_name>
   ```
1. Install the project along with development dependencies:
   ```shell
   uv sync
   ```

# Branching, Committing and Pushing

1. Create a new branch and switch to it:

   ```shell
   git checkout -b <branch_name>
   ```

1. Set the upstream branch for your local branch:

   ```shell
   git push --set-upstream origin <branch_name>
   ```

1. Make necessary changes to the code.

1. If new files are added, stage them:

   ```shell
   git add <file>
   ```

1. Stage the changes in modified files (excluding untracked files):

   ```shell
   git add -uv
   ```

1. Commit the changes:

   ```shell
   git commit -m "Descriptive commit message"
   ```

1. Push the changes to the remote repository:

   ```shell
   git push
   ```

1. Create a merge request on GitLab for the changes to be reviewed and merged.

Note: You need to set your git user name and email to match your GitLab's profile before committing. This only needs to be done once. To do so, run the following commands:

```shell
git config user.name "Your Name"
git config user.email ""
```

# Merging

1. Create a merge request on GitLab for the changes to be reviewed and merged. For merge requests to be merged they need to:
   - be approved by at least one other developer.
   - pass the CI pipeline (static analyzers, tests and docs)
   - have no merge conflicts with the `main` branch.

# Fast-Forward Merge Policy

This repository follows a fast-forward merge policy for merging branches. If the `main` branch has been modified since you created your feature branch, you will need to update your feature branch with the latest changes from `main` before merging.

1. Commit or stash any pending changes in your feature branch.
1. Switch to the `main` branch:
   ```shell
   git checkout main
   ```
1. Pull the latest changes from the main branch:
   ```shell
    git pull
   ```
1. Switch back to your feature branch:
   ```shell
   git checkout <branch_name>
   ```
1. Merge the changes from the main branch into your feature branch:
   ```shell
   git merge main
   ```
1. Resolve any conflicts that may arise during the merge process.

# Pre-commit

To test code quality before comminting, this project utilizes pre-commit hooks. Before making the first commit, follow these steps:

2. Install the pre-commit hooks:
   ```shell
   uv run pre-commit install
   ```

Now, when you attempt to make a commit, the pre-commit hooks will automatically run. If any issues are detected, fix them, stage, and commit again.
For various reason, occasionally, there are different results between local and remote CI results. To override pre-commit locally run: `git commit -m <message> --no-verify`. The CI pipeline takes precedence over the local pre-commit hook.

### Linters

This project uses multiple linters to enforce coding standards. Run the following commands to check for any issues manually (outside of the pre-commit hook):

### Ruff

Check for style violations and potential errors.

```shell
uv run ruff check .
```

### mypy

Check for type hints and type errors.

```shell
uv run mypy ./src
```

# Testing

This project uses `pytest` for automated testing. To run the tests, run the following command:

```shell
uv run pytest .
```

## Code Coverage

This project uses pytest-cov to measure the percentage of code covered by the unit tests. To run the tests and measure the code coverage, run the following command:

```shell
uv run pytest --cov=src
```

Occasionally it is useful to generate a coverage report in html format. It helps to understand what is not covered by the tests. To generate the report, run the following command:

```shell
uv run pytest --cov=src --cov-report html
```

The report will be generated in the `htmlcov` directory.

# Documentation

This project uses mkdocs to generate documentation (following CERN recommendations). To manually generate the documentation, run the following command:

```shell
uv run mkdocs build
```

To view the documentation locally, run the following command:

```shell
uv run mkdocs serve
```

# Continuous Integration (CI)

This project utilizes Continuous Integration to automate various checks and tests. The CI pipeline is configured using GitLab CI/CD. The pipeline consists of the following stages:

### Static Analysis

The static analyzers stage runs various linters to enforce coding standards and maintain code quality. It checks for style violations, potential errors, and security vulnerabilities.

### Tests

The tests stage runs the automated tests for the project. The code coverage measures the percentage of code covered by the tests.

### Documentation

The documentation stage checks for errors during the documentation generation process.

Please note that it is not possible to merge to the main branch without a successful CI pipeline.

# Versioning

Version information is available at [CHANGELOG.md](CHANGELOG.md) file.

When a new version is released, the following steps should be taken:

1. Members of the team should agree on the new version number according to https://semver.org/spec/v2.0.0.html.
1. Update the version number in the [CHANGELOG.md](CHANGELOG.md) file.
1. Describe the changes in the [CHANGELOG.md](CHANGELOG.md) file. Tip: check Merge Requests titles for hints on what to include.
1. Update the version number in the \`src/<name>/**init**.py\`\` file.
1. Commit the changes.
1. Create a new Merge Request entitled "Release version \<version_number>".
1. Once the Merge Request is approved and merged, create a new tag using the GitLab UI. The tag should be named "\<version_number>". Always tag the main branch.

## Adding or removing dependencies

```shell
uv add package-name
```

This will automatically update the `pyproject.toml` and the `uv.lock` file and install the new package.

```shell
uv remove package-name
```

This will automatically update the `pyproject.toml` and the `uv.lock` file and remove the package.

Uv sync has the following options:

```shell
uv sync --help
# --locked                Assert that the `uv.lock` will remain unchanged [env: UV_LOCKED=]
# --frozen                Sync without updating the `uv.lock` file [env: UV_FROZEN=]
# --no-dev                Disable the development dependency group
# --no-editable           Install any editable dependencies, including the project and any workspace members, as non-editable
# --no-install-project    Do not install the current project
# --extra <EXTRA>         Include optional dependencies from the specified extra name
```

Documentation available at [uv sync docs](https://docs.astral.sh/uv/reference/cli/#uv-sync)
