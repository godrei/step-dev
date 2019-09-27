# Step outputs

## Step Output ID and Title naming

Use all-upper-case [snake case](https://en.wikipedia.org/wiki/Snake_case) style output IDs, e.g. `OUTPUT_PATH`.

## Outputs with list of values

You should postfix the output ID with `_LIST` (e.g. `OUTPUT_PATH_LIST`), and provide the values as a newline character (`\n`) separated list (e.g. `first value\nsecond value`).

This is not a hard requirement, but a strong suggestion. This means that you should prefer this solution unless you really need to use another character for separating values

Based on our experience the newline character (`\n`) works really well as a universal separator character, as it's quite rare in output values (compared to `,`, `;`, `=` or other more common separator characters).
