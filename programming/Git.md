# GIT

## Useful commands

### Remove all branches except master

    git branch | grep -v "master" | xargs git branch -D

### Get branches ordered by recent commits

    git branch --sort=-committerdate  # DESC
    git branch --sort=committerdate  # ASC

## Using Husky

### Hook to prevent pushing to master

    git branch | grep "*" | egrep -v "^* master$"

Source: https://stackoverflow.com/questions/53726982/setup-pre-push-hook-with-husky-to-prevent-pushing-to-master-branch
