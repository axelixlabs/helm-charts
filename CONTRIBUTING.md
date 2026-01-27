# Contributing Guidelines

Contributions are welcome via GitHub pull requests. This document outlines the process to help get your contribution accepted.

## How to Contribute

Here is step-by-step process of what we expected to be done in case you want to contribute.

### 1. Fork this repository

First of all, of course, the repository must be forked.

### 2. Branch naming convention

If you're solving a particular issue on GitHub, then we expect the branch to follow the naming convention `feature/GH-<ISSUE_NUMBER>`, for example `feature/GH-75`. If you're just want to introduce a minor polishing, then there is no need to submit a ticket for it - just introduce a branch with the name that you think correctly reflects the changes made.

### 3. Management of the changes

Now, **chart releases are immutable**. Any change to a chart warrants a chart version bump even if it is only changed to the documentation. So, if you have:

- Changed the default values
- The Go templates
- Even just the documentation

Then please, upgrade the chart's `version`. The chart's `version` should follow [semver](https://semver.org/) versioning schema, so any breaking (backwards incompatible) change requires the major version bump. We also expect the appropriate migration guide in the `README.md` for this chart.

### 4. Open a pull request

Finally, open the PR and sign the CLA

### 5. Pass the review process

Once changes have been merged, the release job will automatically run to package and release changed charts.

### Community Requirements

This project is released with a [Contributor Covenant](https://www.contributor-covenant.org).
By participating in this project you agree to abide by its terms.