# GIT

## Useful commands

### Remove all branchs except master

    git branch | grep -v "master" | xargs git branch -D

### Get branches ordered by recent commits

    git branch --sort=-committerdate  # DESC
    git branch --sort=committerdate  # ASC
