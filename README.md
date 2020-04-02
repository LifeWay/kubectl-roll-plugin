# kubectl-roll-plugin

## Purpose

`kubectl roll` is a [Kubernetes](https://kubernetes.io/docs/home/) client-side plugin that will "roll" through deleting a target namespace's pods, one by one. In between pod deletions, it will sleep for a default of 30 seconds (or for a number of seconds that you provide). You can also supply a label within that namespace to further target the pods to be deleted.

## Installation

**Requires [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/) v1.12 or higher**

1. Clone repo or copy the 2 files from this repo into the same folder on your computer
2. Run `./install` from the repo directory

*Note: Only tested on macOS Mojave*

## Usage

`kubectl roll -n {namespace} {seconds}`

or

`kubectl roll -n {namespace} -l {label} {seconds}`

Ex.

`kubectl roll -n api-prod 15`

or

`kubectl roll -n api-prod -l name=shipping-api 15`

- You are required to provide the target namespace name and can optionally provide the number of seconds to sleep in between each pod deletion. If you do not specify a `seconds` argument, the default is 30.
- Your current kubeconfig context will be used for the plugin's execution.
- You can also use `namespace` or `ns` in place of `-n` and `--selector` in place of `-l`.

## Semantic Releases

This plugin follows [SemVer](https://semver.org/). The [semantic-release](https://github.com/semantic-release/semantic-release) library is used to manage version numbers, cut GitHub releases, and create/update the [changelog](CHANGELOG.md). The commit message format determines the release number and is enforced with a [pre-commit hook](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) (implemented via [husky](https://github.com/typicode/husky)). Commit messages must adhere to the guidlines outlined by the [Angular project](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines). Here is an example of the release type that will be created based on the commit message:

| Commit message                                                                                                                                                                                   | Release type               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| `fix(pencil): stop graphite breaking when too much pressure applied`                                                                                                                             | Patch Release              |
| `feat(pencil): add 'graphiteWidth' option`                                                                                                                                                       | ~~Minor~~ Feature Release  |
| `perf(pencil): remove graphiteWidth option`<br><br>`BREAKING CHANGE: The graphiteWidth option has been removed.`<br>`The default graphite width of 10mm is always used for performance reasons.` | ~~Major~~ Breaking Release |
