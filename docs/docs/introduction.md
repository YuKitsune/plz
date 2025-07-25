---
sidebar_position: 1
sidebar_label: Introduction
---

# Introduction

plz is a dead-simple task runner with a familiar POSIX-style interface.
It's lightweight, easy to use, and perfect for consolidating project-specific tasks.

## Features

- Designed from the ground-up as a command runner without the constraints of a build tool.
- Supports Windows, macOS, and Linux, and isn't dependent on a specific Shell.
- Provides a POSIX-style command-line interface allowing for nested subcommands, and variable substitution using command-line arguments.
- Uses a simple YAML file for configuration.

## Overview

:::warning
[;z] is still in early development and it's configuration syntax and usage are subject to change.
:::

plz relies on YAML for its configuration.

In your `plz.yaml`, you can define variables at the root level.
These variables are global, so they're available to all commands and subcommands throughout the file.

Example:
```yaml
variables:
  name: Godzilla

commands:
  greet:
    action: echo Hello, $name!

  pet:
    action: echo You have petted $name!
```

```sh
$ plz greet
Hello, Godzilla!

$ plz pet
You have petted Godzilla!
```

You can also define variables within commands.
These variables are available to the command and its subcommands.

```yaml
commands:
  greet:
    variables:
      name: Godzilla
    action: echo Hello, $name!

  pet:
    variables:
      name: Maxwell
    action: echo You have petted $name!
```

```sh
$ plz greet
Hello, Godzilla!

$ plz pet
You have petted Maxwell!
```

Actions represent the actual commands that get executed.
When you invoke a command, its actions are run in sequence.

```yaml
commands:
  greet:
    variables:
      name: Godzilla

    # Single action
    action: echo Hello, $name!

  pet:
    variables:
      name: Maxwell

    # Multiple actions
    actions:
      - echo Petting $name...
      - sleep 5
      - echo You have petted $name!
```

```sh
$ plz greet
Hello, Godzilla!

$ plz pet
Petting...
You have petted Maxwell!
```

## Learn more

Interested in learning more? [Install plz](./installation.md) and try it out!
