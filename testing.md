# Step testing

Step's unit testing possibilities depends on the used programming language.

This document will cover how the step's end-to-end / integration test can be done.

Steps can be activated in three ways in workflows:

- Step from a StepLib
- Step from direct url
- Step from local path

During step development running a step from its local file path is the best approach. When you reached a state which you want to mark a stable version of the step you push that version into a step repository and you can test that step version using the step repository's url.

If the step would be useful for others too, you can share it to a StepLib, like the [official Bitrise StepLib](https://github.com/bitrise-io/bitrise-steplib.git) and use your step from the StepLib.

## Step from a StepLib

If you use a step from a step collection / library then a step's ID consists of three parts:

1. The step-lib source
2. The step's ID in the step-lib
3. The step's version, registered in the step-lib

```YAML
format_version: 9

workflows:
  primary:
    steps:
      - https://github.com/bitrise-io/bitrise-steplib.git::script@0.9.0:
          title: "Full ID"
          inputs:
          - content: |
              #/bin/bash
              echo "Welcome to Bitrise!"
```

If you define a `default_step_lib_source` (just like you can see it at the top of this bitrise.yml file) then you don't have to specify it again for the steps if you want to use the default_step_lib_source.

```YAML
format_version: 9
default_step_lib_source: https://github.com/bitrise-io/bitrise-steplib.git

workflows:
  primary:
    steps:
      - script@0.9.0:
          title: "Using default_step_lib_source"
          inputs:
          - content: |
              #/bin/bash
              echo "Welcome to Bitrise!"
```

If you want to use the latest version of the step you can even remove the version from the ID.
Note that the trailing colon is still required, even if you don't specify the version!

```YAML
format_version: 9
default_step_lib_source: https://github.com/bitrise-io/bitrise-steplib.git

workflows:
  primary:
    steps:
      - script:
          title: "Using latest version"
          inputs:
          - content: |
              #/bin/bash
              echo "Welcome to Bitrise!"
```

## Step from direct url

This workflow shows how to use steps with specifying the step's git clone URL directly.
This way the step will always be git cloned from the specified URL and not used from a step library/collection.
To do this you have to construct the ID in this way: `git::git-clone-url-of-the-step-repo@branch-or-tag`

```YAML
format_version: 9

workflows:
  primary:
    steps:
      - git::https://github.com/bitrise-steplib/steps-timestamp.git@master:
          title: "remote_git-stamp-test"
```

## Step from local path

You can specify local path for a step as well.
The path can be any kind of path (even absolute path) but the best way is to use relative paths if you want to run your workflow on a Continuous Integration service or want to share with someone else.

Absolute paths and relative-to-home paths most likely won't work anywhere else except on your machine.
To do this you have to construct the ID in this way: `path::local-path-of-the-step-folder`

```YAML
format_version: 9

workflows:
  primary:
    steps:
      - path::./steps-timestamp:
          title: "relative_pth-stamp-test"
```
