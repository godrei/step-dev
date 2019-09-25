# Step inputs

## Never depend on Environment Variables in your Step

You should expose every outside variable as an input of your step,
and just set the default value to the Environment Variable you want to use in the `step.yml`.

An example:

The Xcode Archive step generates a `$BITRISE_IPA_PATH` output environment variable.
**You should not** use this environment variable in your Step's code directly,
instead you should declare an input for your Step in `step.yml` and just set the default
value to `$BITRISE_IPA_PATH`. Example:

```YAML
- ipa_path: "$BITRISE_IPA_PATH"
  opts:
      title: "IPA path"
```

After this, in your Step's code you can expect that the `$ipa_path` Environment Variable will
contain the value of the IPA path.

By declaring every option as an input you make it easier to test your Step,
and you also let the user of your Step to easily declare these inputs,
instead of searching in the code for the required Environment Variable.

## Step Input ID and Title naming

Use lower case [snake case](https://en.wikipedia.org/wiki/Snake_case) style input IDs, e.g. `project_path`.

Step input's title should be short and descriptive sentence/half sentence: `The Xcode project's path`.

Step input's title should not be the flag controlled by the step input, as one of the main advantage of using steps is you do need to know how the given tools/service works, you just need to configure steps.

The input key can not be `opts` (as it is used for the input’s options).

## Step input values

Step input values are strings as Bitrise CLI exposes the step inputs as Environment variables to the steps.

If your input accepts a boolean value, use `value_options` with `"yes" and "no"` possible values, double quote character `"` is important.

## Value options

If the input can accept a fix set of values, the input's `value_options` property to list the possible values. Input with value option needs to be marked as `required` and needs to have default value.

## Secret environment variables in Steps

You can mark Step inputs as **Sensitive** to make sure their values do not get exposed. Sensitive inputs only accept [Secrets](/bitrise-cli/secrets/) - secret environment variables - as values. This ensures they are not visible in build logs.

To mark a Step input as sensitive, use the `is_sensitive` property. It has two values: `true` and `false`.

Please note that if you mark an input as sensitive, the `is_expand` property of the input also must be `true`!

```YAML
inputs:
  - certificate_urls: $BITRISE_CERTIFICATE_URL
    opts:
      title: "Certificate URL"
      is_sensitive: true
```

## Inputs which can accept a list of values

You should postfix the input ID with `_list` (e.g. `input_path_list`), and expect the values to be provided as a newline character (`\n`) separated list (e.g. `first value\nsecond value`).

This is not a hard requirement, but a strong suggestion. This means that you should prefer this solution unless you really need to use another character for separating values. Based on our experience the newline character (`\n`) works really well as a universal separator character, as it's quite rare in input values (compared to `,`, `;`, `=` or other more common separator characters).

**As a best practice you should filter out empty items**, so that `first value\n\nsecond value` or even

```YAML
first value\n       \nsecond value
```

is treated the same way as `first value\nsecond value`. Again, not a hard requirement, but based on our experience this is the most reliable long term solution.

## Step input categories

Step input `category` can be used to group similar inputs. Inputs with the same `category` are collapsed under the category name on the Workflow Editor.

Leave required input without category even if it has default value.

The suggested maximum number of inputs in a group or in the root is 6. This amount of input can fit in a full screen website design without scrolling.

Use category only if the step has more than 6 input and if you can put multiple inputs in a given category, so do not add category for only one input.

## The order of inputs

Step inputs are presented in the order as they appear in the `step.yml`, required and frequently used inputs should be the first ones. The rest of the inputs is in order of the importance.
