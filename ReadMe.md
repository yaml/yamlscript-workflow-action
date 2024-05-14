yaml/yamlscript-workflow-action
===============================

GitHub Action to enable writing workflows in YAMLScript


## Usage

Create a workflow shim file called `.github/workflows/<name>.yaml`
that looks like this:

```yaml
on: push
jobs:
  workflow:
    runs-on: ubuntu-latest
    steps:
    - uses: yaml/yamlscript-workflow-action@main
#     with: {ys-file: .github/workflows/<other-name>.ys}
```

Then create a YAMLScript file called using the same file path, except
change the `.yaml` extension to `.ys`.

```yaml
--- !yamlscript/v0

gh =: slurp('/github.json').json/load()

say: "Hello $(ENV.USER)!"
say: "Workflow file: '$(gh.workflow)'"

shell::
  make test
```


## Overview

Using this workflow does the following things before running your
intended YAMLScript workflow file:

* Checks out your target repo (with actions/checkout@v4)
* Installs the `ys` YAMLScript CLI interpreter
* Writes the big mapping of workflow related data to
  `.github/github.json`
  * You can load this file from YAMLScript to access any relevant data


## See Also

An example repo using this action is
https://github.com/ingydotnet/gha-yamlscript-workflow-example


## Copyright and License

Copyright 2024 by Ingy döt Net

This is free software, licensed under:

The MIT (X11) License
