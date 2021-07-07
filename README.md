# GitHub Runner

-----------
GitHub allows developers to run GitHub Actions workflows on your own runners.
This Docker image allows you to create your own runners on Docker.


## Important notes

* GitHub [recommends](https://help.github.com/en/github/automating-your-workflow-with-github-actions/about-self-hosted-runners#self-hosted-runner-security-with-public-repositories) that you do **NOT** use self-hosted runners with public repositories, for security reasons.
* Organization level self-hosted runners are supported (see environment variables), but be advised that the GitHub API for organization level runners is still in public beta and subject to changes.

Create a `.env` to provide environment variables when using docker-compose :
```
RUNNER_REPOSITORY_URL=https://github.com/your_url/your_repo
# or RUNNER_ORGANIZATION_URL=https://github.com/your-organization
GITHUB_ACCESS_TOKEN=the_runner_token
```


## Runner Token

In order to link your runner to your repository/organization, you need to provide a token. There is two way of passing the token :

* via `GITHUB_ACCESS_TOKEN` (recommended), containing a [Personnal Access Token](https://github.com/settings/tokens). This token will be used to dynamically fetch a new runner token, as runner tokens are valid for a short period of time.
  * For a single-repository runner, your PAT should have `repo` scopes.
  * For an organization runner, your PAT should have `admin:org` scopes.
* via `RUNNER_TOKEN`. This token is displayed in the Actions settings page of your organization/repository, when opening the "Add Runner" page.
