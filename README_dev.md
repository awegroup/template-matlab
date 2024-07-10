# Introduction

Hi! Welcome to this MATLAB Repository Template, this `README_dev.md` contains instructions on the intended usage of this MATLAB template.

## Getting-Started
1. Create a new repository from this template following the [GitHub instructions](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)
2. Clone the repository to your local machine
3. Make some changes, and create your first commit see: ...

## Setting-Up the Project
1. If you use MATLAB Addons, document these in the `DEPENDENCIES.txt` file. If you are unsure, call the function `src/utils/check_dependencies.m` to check for the required dependencies.

## Proposed-Workflow

### General recommendations
- It is recommended to work with both a `main` and specific `feature` branches. If your development workflow requires the `main` to be available for users, consider adding a `develop` to test new versions before merging to `main`. For more information, consult the [AWE developer guides](https://awegroup.github.io/developer-guide/docs/branch-management.html).
- Write user settings in a `.yaml` file
- Don't use any hardcode inside your source folder
- Write scripts that should be run insidethe folder `scripts`/
- The other folders should only contain functions or data

### Steps for developing and prototyping new features
1. Create an issue on GitHub
2. Create a new branch from this issue
3. Checkout the branch locally and develop your new feature
4. If you are working with multiple developers or require a code review, create a pull-request to merge and close this issue
5. Once merged, delete the feature branch
6. Update branch information locally using `git fetch --prune`, pull in new info `git pull origin develop` and delete branch locally using `git branch -d <enter branch name>`


## Testing

To run the tests in MATLAB, use the following command:
```matlab
results = runtests('tests', 'IncludeSubfolders', true)
```

For more information on testing in MATLAB, see the [AWE Developer Guides](https://awegroup.github.io/developer-guide/docs/testing.html#testing-in-matlab).

## Documentation
The documentation is build with sphinx, a Python documentation generator.

To build the documentation, run the following command in the root of the repository:
```bash
sphinx-build -b html docs/ docs/_build/
```

## GitHub Actions
To make use of the GitHub Actions that depend on MATLAB, the visibility of the repository will need to be set to **public**. 

In case the repository needs to remain private, you will need to request a Batch Token (pilot program) from MathWorks to use MATLAB in a private repository. To request a token, fill out the [MATLAB Batch Token From](https://nl.mathworks.com/support/batch-tokens.html). To use the batch token, add the token as a repository secret with the name `MLM_LICENSE_TOKEN` and update the workflow file `.github/workflows/testing.yml` with the token by adding an environment variable `MLM_LICENSE_TOKEN` with the value of the token. Your workflow file should then look like this:

```yaml
name: Generate Test and Coverage Artifacts

on:
  push:
    branches: [ "main", "develop" ]
  pull_request:
    branches: [ "main", "develop" ]
  workflow_dispatch:
env:
  MLM_LICENSE_TOKEN: ${{ secrets.MLM_LICENSE_TOKEN }}
jobs:

```

## Explanation of folders/files

- `.gitkeep` is added to empty folders in order for git to be able to track them. Without this file, the folder would be automatically ignored and the project structure would not be clear. Once other files are present inside this folder, this file can be deleted.
- The folders `data/`, `data_processed/`, and `results/` have been added to the `.gitignore` file by default, as they are expected to contain 
  - large files that should not be uploaded to GitHub
  - confidential data that should not be uploaded to GitHub
  - generated data that can be recreated (within reasonable time)
  - generated results that can be recreated (within reasonable time)