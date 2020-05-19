# kubectl-roll-plugin

## Purpose

`kubectl roll` is a [Kubernetes](https://kubernetes.io/docs/home/) client-side plugin that will "roll" through deleting a target namespace's pods by targeting the StatefulSets, DaemonSets, and Deployments in that namespace. Any standalone pods in the namespace will be ignored and a warning will display to notify the user of the number of pods in the namespace that were not restarted.

## Installation

**Requires [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/) v1.12 or higher**

1. Clone repo or copy the 2 files from this repo into the same folder on your computer
2. Run `./install` from the repo directory

*Note: Only tested on macOS Mojave*

## Usage

`kubectl roll -n {namespace}`

Ex.

`kubectl roll -n api-prod`

- You are required to provide the target namespace name.
- Your current kubeconfig context will be used for the plugin's execution.
- You can also use `--namespace` in place of `-n`.

## Semantic Releases

This plugin follows [SemVer](https://semver.org/). The [semantic-release](https://github.com/semantic-release/semantic-release) library is used to manage version numbers, cut GitHub releases, and create/update the [changelog](CHANGELOG.md). The commit message format determines the release number and is enforced with a [pre-commit hook](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) (implemented via [husky](https://github.com/typicode/husky)). Commit messages must adhere to the guidlines outlined by the [Angular project](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines). Here is an example of the release type that will be created based on the commit message:

| Commit message                                                                                                                                                                                   | Release type               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| `fix(pencil): stop graphite breaking when too much pressure applied`                                                                                                                             | Patch Release              |
| `feat(pencil): add 'graphiteWidth' option`                                                                                                                                                       | ~~Minor~~ Feature Release  |
| `perf(pencil): remove graphiteWidth option`<br><br>`BREAKING CHANGE: The graphiteWidth option has been removed.`<br>`The default graphite width of 10mm is always used for performance reasons.` | ~~Major~~ Breaking Release |
