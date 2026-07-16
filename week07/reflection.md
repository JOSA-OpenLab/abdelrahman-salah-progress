# Week07

## task 1

For task 1, I added a dependabot configuration to a fastAPI project, here is the config file:

```yaml
version: 2

updates:
  - package-ecosystem: "uv"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

  - package-ecosystem: "docker"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10

```

I am using uv as a package manager for python, and I added docker and github-actions to the config file to keep them up to date as well. I also set the schedule to weekly and limited the number of open pull requests to 10.

after running it for the first time, I got a lot of pull requests for multiple dependencies, so I had to merge them and make my project more secure. I also learned that dependabot can be configured to ignore certain dependencies or versions, which can be useful if you want to avoid breaking changes.

## task 2

## task 3

## task 4
