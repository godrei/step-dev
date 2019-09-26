# Share process

- share
- restart the share

To share your step to a StepLibrary you need to do the following:

- fork the StepLib repository
- git the forked StepLib repository
- place your new version's step.yml into <STEPLIB_FORK_REPO>/steps/<STEP_ID><STEP_VERSION>/ directory
- add `published_at` property to the step.yml with the following format: `2018-08-22T09:43:08.222832748Z`
- add the `source` field with `git` and `commit` fields

```YAML
published_at: 2018-08-22T09:43:08.222832748Z
source:
  git: https://github.com/bitrise-io/steps-activate-ssh-key.git
  commit: 29e73e8056a05ecf681ddac659afcfe9f3385a9e
```

## share-this-step-workflow

## stepman share
