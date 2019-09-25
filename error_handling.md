# Error handling

Steps should set non-zero exist status in case of an error occurs during step run.

By default if a step fails in a workflow, subsequent steps will not be executed. This default behavior fits good for most of the step, for example if `Xcode archive` fails, it does not makes sense to run `Deploy to iTunes Connect`.

However there is an option to override this behavior and mark a step skippable. If you set `is_skippable` property on a step its non-zero exist status will not mark a build failed.

For example cache pull and push steps are marked as skippable as usually it does not mean that your code change is not integrable, or your project is in inconsistent state.
