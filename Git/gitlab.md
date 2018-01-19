# GitLab

## GitLab CI/CD

* [GitLab CI/CD Feature](https://about.gitlab.com/features/gitlab-ci-cd/)
* [CI/CD Documentation](https://docs.gitlab.com/ee/ci/)
* [CI/CD Quick Start](https://docs.gitlab.com/ee/ci/quick_start/)
* [`.gitlab-ci.yml` documentation](https://docs.gitlab.com/ee/ci/yaml/README.html)
* [GitLab Runners](https://docs.gitlab.com/ee/ci/runners/README.html)
* [Official GitLab Runner](https://docs.gitlab.com/runner/)
* [Testing PHP Projects](https://docs.gitlab.com/ce/ci/examples/php.html)

## Quick Start Notes

GitLab CI service can be used by adding a `.gitlab-ci.yml` to the root directory of a repository and configuring the GitLab project to use a Runner. This will then trigger the CI pipeline for each commit or push. By default a pipeline is run with [three stages](https://docs.gitlab.com/ee/ci/yaml/README.html#stages): `build`, `test`, and `deploy`, although it isn't necessary to use all three stages.

When a pipeline runs successfully (no non-zero return values), then a green checkmark is added to the associated commit, helping to highlight if a commit was the cause of an issue or not.

### What is `.gitlab-ci.yml`

