---
sidebar_label: 'Start here'
sidebar_position: 1
---
# Prerequisites

The command module represents the Fairy module allowing users to interact directly with services, repositories and any sort of handler via the logistic of commands. This feature is predominantly used in bots (Discord, Slack, Telegram, etc...), in shell applications (trading automations etc...) and in Game servers (Minecraft, Rust, etc..).

## Adding the command module


In your module build.gradle, please add the following dependency:

```groovy
dependencies {
    api("io.fairyproject:module.command")

    // Other dependencies
}
```

If you are using **Bukkit**, you may add instead:

```groovy
dependencies {
    api("io.fairyproject:bukkit-command")

    // Other dependencies
}
```

Tada! You're all set. Lets create your first command 👍 
