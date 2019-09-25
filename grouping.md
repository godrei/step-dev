# Step Grouping convention

You can use `project_type_tags` and `type_tags` to group/categorize your steps.

`project_type_tags` are used to control if the step is available/useful for the given project type.

Available `project_type_tags`:

- ios
- macos
- android
- xamarin
- react-native
- cordova
- ionic
- flutter
- web

_If step is available for all project types, do not specify project_type_tags, otherwise specify every project types, with which the step can work._

`type_tags` are used to categorize the steps based on it's functionality.

Available `type_tags`:

- access-control
- artifact-info
- installer
- deploy
- utility
- dependency
- code-sign
- build
- test
- notification

_Every step should have at least one type_tag, if you feel you would need a new one, or update an existing name, please [create a github issue](https://github.com/bitrise-io/bitrise/issues/new), with your suggestion._
