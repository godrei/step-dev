# Step Title, Description and Summary

The `step.yml`'s `title`, `description` and `summary` fields are used to describe the given step. These metadata present both on the Workflow Editor and in the Bitrise CLI tools.

## Title (required)

Short and descriptive: who knows the underlying service/tool should understand what is the purpose of the step.
Not a noun, but an activity/verb: `Script Runner` -> `Run Script`.

The title should consist by the underlying tool/service and the action performed, like: `Git clone`, `Xcode archive` or `Deploy to Bitrise.io`.

Do not include platform in the title as `project_type` tag contains this information: `Xcode archive for mac` -> `Xcode archive`.

Avoid using step word in the title: `Git clone step` -> `Git clone`.

Use correct tool and service names: `Github` -> `GitHub`.

Do not include implementation details in the title: `Xcode archive using xcodebuild` -> `Xcode Archive`.

Use `[Beta]` prefix for new steps where impossible to identify all possible edge cases at the first development stage or if the underlying tool/service is in alpha or beta stage only.

## Description (optional)

Used to explain the step, what it does, which service/tool, which action/endpoint is used by the step.
This should be the longest explanation of the step, by reading this users needs to be able to understand the step's purpose and boundaries without reading the source code.

By default the step's description is collapsed on the Workflow Editor and the `summary` is presented.

## Summary (required)

A single line of the most significant infos about the step, can not consist by more than 100 chars.

The summary is visible by default on the Workflow Editor, by expanding the summary, the step's `description` will be presented if any.
