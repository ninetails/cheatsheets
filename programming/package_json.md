# package.json settings & scripts

## npm exposed variables

> See: https://gist.github.com/moos/4635bda5b04dc8113d8ea7ee974cabc2

### Notes about `$npm_execpath`

I like to use it as a wildcard between `npm` and `yarn`. It uses what user called when executed a npm script.

## `yarn reset`

> Requires: Yarn & Lerna

Remove, clean and install all dependencies on a Yarn Workspaces w/ Lerna environment.

```
{
  ...
  "scripts": {
    ...
    "clean": "lerna clean --yes 2>/dev/null || :",
    "purge": "$npm_execpath run lerna:clean && $npm_execpath run clean && rm -rf node_modules",
    "reset": "$npm_execpath run purge && $npm_execpath install",
    ...
  }
}
```

Run

```bash
$ yarn reset
```

### About

#### clean

Runs npm script `clean` on every package that have it. Each one should provide what to do (things like remove build folders etc)

#### purge

Runs script above; `lerna clean` to remove/clean dependencies installed on each package and finally removes root `node_modules`

#### reset

Runs purge and then `yarn install`.

## configure gitflow-avh

> Requires: gitflow-avh
> Optional: npm-run-all

If you don't want to use `npm-run-all` just change below.

```
{
  ...
  "scripts: {
    ...
    "git:flow": "command -v git-flow >/dev/null 2>&1 && [[ -z \"$(git config --get-regexp gitflow.prefix)\" ]] && NPM_EXECPATH=$npm_execpath npm-run-all git:flow:init git:flow:config || :",
    "git:flow:init": "git flow init -fd",
    "git:flow:config": "NPM_EXECPATH=$npm_execpath npm-run-all git:flow:config:*",
    "git:flow:config:hotfix": "git config gitflow.prefix.hotfix 'fix/'",
    "git:flow:config:feature": "git config gitflow.prefix.feature 'feature/'",
    "git:flow:config:release": "git config gitflow.prefix.release 'release/'",
    "git:flow:config:bugfix": "git config gitflow.prefix.bugfix 'bugfix/'",
    "git:flow:config:support": "git config gitflow.prefix.support 'support/'",
    "postinstall": "$npm_execpath run git:flow",
    ...
  }
}
```

### About

#### `command -v git-flow >/dev/null 2>&1`

Checks if user have [git-flow](https://github.com/petervanderdoes/gitflow-avh) executable installed and execute next command.

#### `[[ -z \"$(git config --get-regexp gitflow.prefix)\" ]]`

Checks if there's no `gitflow.prefix.*` config set.

#### `git flow init -fd`

Initialize gitflow with defaults.

#### `git:flow:config:*`

Sets defaults due this [issue](https://github.com/petervanderdoes/gitflow-avh/issues/393).

#### `postinstall`

> See: https://docs.npmjs.com/misc/scripts
