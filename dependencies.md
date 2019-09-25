# Step dependencies

In the context of Steps, dependency means an executable or a library needed to be executed or utilized by the step.

A step dependency is installed by the `Bitrise CLI` if it is not available in the PATH environment variable. Unused dependencies increase the build time unnecessarily.

Since steps can be performed in any environment where the Bitrise CLI can run, list every used dependency, even if you know that they are pre-installed on the Bitrise stacks.

Step dependencies should not include [toolkit](https://github.com/bitrise-io/bitrise/blob/master/_docs/bitrise-yml-format-spec.md#step-properties) dependencies, as the Bitrise CLI will take care of installing those automatically.

For example:

_A step written in `Go` should not list `Go` as a dependency if the step uses the `Go Bitrise CLI toolkit`_

Bitrise CLI can install step dependencies available in the Homebrew package manager:

```YAML
deps:
  brew:
  - name: cmake
```

apt-get dependencies available in sources listed in `sources.list` file on the host machine:

```YAML
deps:
  apt_get:
  - name: cmake
```

Steps can define dependencies which need to be available on the host machine but cannot be installed in an easy way (like using a single brew or apt-get command):

```YAML
deps:
  check_only:
  - name: xcode
```

Currently, the only supported `check_only` dependency is `xcode`.

Other dependencies need to be installed and checked while the step is running or using other steps.

## Submodules

As a Step runs frequently in a CI / automation environment you should try to make your Step as stable as possible.
This includes the resources / tools used by your Step as well, not just the core code.

If your Step depends on another tool, which have to be downloaded on-demand, during the execution
of your Step, there's a chance that even your Step was retrieved correctly but the
resource it tries to download just fails because of a network, authorization or other error.

You should try to include everything what's required for your Step into the Step's repository.
In case of submodules, you should rather include the content of the other repository,
instead of actually using it as a submodule.

The only exception is the dependencies you can fetch from an OS dependency manager,
on Debian systems you can use `apt-get` and on OS X you can use `brew`.
You can declare these dependencies in your `step.yml`, with the `deps` property,
and `bitrise` will manage to call the dependency manager to install the dependency,
and will fail before the Step execution in case it can't retrieve the dependency.
