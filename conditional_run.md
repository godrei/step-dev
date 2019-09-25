# Condition based step run

## is_always_run

By default if a step fails in a workflow, subsequent steps will not be executed. This default behavior fits good for most of the step, for example if `Xcode archive` fails, it does not makes sense to run `Deploy to iTunes Connect`.

However for some types it definitely makes sense to run regardless the workflow's run status, to modify this behavior you can set `is_always_run` property of the step.

This is a recommended settings for every steps with `notification` `type_tags`, to be able to send a notification about failed builds as well.

## run_if

If you want to run a step if certain condition applies, you can use the step's `run_if` to define the run condition.
The Bitrise CLI repository contains useful [examples](https://github.com/bitrise-io/bitrise/blob/master/_examples/experimentals/templates/bitrise.yml).
