# GitHubApi.groovy

A simple Groovy script to provide Groovy access to the GitHub API. I'm not making any claims to be the best Groovy programmer around. I just tend to use Groovy for scripting on occasion and wanted to be able to script against the GitHub API.

The API object provided by this script will fetch all data requested, even if the data are paged. It will also respect GitHub's rate limits and sleep when necessary to avoid exceding those limits. The personal access token is necessary, since GitHub understandably limits the number of anonymous REST calls allowed.

## Installation

While you could clone this repository, that's not necessary. You can simply copy the contents of the [raw GitHubApi.groovy file](https://raw.githubusercontent.com/bmamlin/GitHubApi.groovy/master/GitHubApi.groovy) into an editor and save it as GitHubApi.groovy wherever you keep your Groovy scripts.

## Setup

To use this script, you need to have (or create) a personal access token (GitHub Settings > Personal access tokens) and place it into a file named `.github.token` in your home folder (i.e., `~/.github.token`).

## Usage

```groovy
#!/usr/bin/env groovy

def github = new GitHubApi()

// Find all OpenMRS repositories whose name starts with "openmrs-module-"
repos = github.get('/orgs/openmrs/repos').findAll {
	it.name.startsWith('openmrs-module-')
}

// List names of repositories
println repos.collect{ it.name }.join(', ')
```

## Methods

| Method | Description |
|--------|-------------|
| .get(path[, query]) | Get resource at `path` without option parameters in `query` hash |
| .put(path, body) | Put the contents of `body` to a resource at `path` |
| .patch(path, body) | Patch the resource at `path` with the contents of `body` |

The GitHub API is well-documented [here](https://developer.github.com/v3/).
