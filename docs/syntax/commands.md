---
sidebar_label: 'Commands'
sidebar_position: 1
---

Creating Custom Commands in Skript
Welcome to the comprehensive guide on crafting custom commands in Skript. This powerful tool allows you to tailor your server experience by creating commands that perform a wide array of actions. Whether you're looking to broadcast messages, manage players, or interact with the world, mastering commands is your first step. This guide will walk you through the structure of a command and how to write one.

Understanding Command Structure
Before diving into creating your command, it's crucial to understand its structure. A command in Skript is more than just a word; it's a set of instructions and parameters that define how the command behaves and who can use it. Here's a breakdown of the command structure:

Patterns: Defines the syntax of the command. It usually starts with the command keyword followed by parameters enclosed in angle brackets.
Required Entries: These are essential for the command to function. Typically, this includes the trigger.
Optional Entries: These entries provide additional control and customization to your command. They include usage, description, prefix, permission settings, aliases, executable context, cooldown settings, and cooldown messages.
Crafting Your First Command
Step 1: Define the Basic Structure
Start with the basic outline of your command. Define the pattern and the trigger. The pattern includes the command and its parameters. For example:

```js
command /greet <player>:
    trigger:
        # Your code goes here
```

Step 2: Add Descriptions and Usage Information
Provide clear descriptions and usage guidelines. This helps users understand what your command does and how to use it.

```js
command /greet <player>:
    description: Sends a greeting to the specified player.
    usage: /greet <player> - Greets a player.
    [...]
```

Step 3: Set Permissions and Aliases
Define who can use the command and any alternative ways to call it (aliases). Permissions ensure that only authorized users can execute the command.

```js
command /greet <player>:
    [...]
    permission: skript.greet
    permission message: You do not have permission to greet players.
    aliases: /hello, /hi
    [...]
```

Step 4: Configure Execution Context and Cooldowns
Specify whether the command can be used by players, the console, or both. Additionally, set cooldowns to prevent spamming of the command.

```js
command /greet <player>:
    [...]
    executable by: players and console
    cooldown: 10 seconds
    cooldown message: Wait %remaining time% before greeting again.
    cooldown bypass: skript.greet.bypass
    cooldown storage: {greet_cooldown::%uuid of player%}
    [...]
```

Step 5: Script the Trigger
The trigger section is where the action happens. This is where you script what the command does when executed.

```js
command /greet <player>:
    [...]
    trigger:
            send "Hello, %argument%" to the player
```

Step 6: Test Your Command

As a final result, you should obtain something that looks relatively like this:
```js
command /greet <player>:
    description: Sends a greeting to the specified player.
    usage: /greet <player> - Greets a player.
    permission: skript.greet
    permission message: You do not have permission to greet players.
    aliases: /hello, /hi
    executable by: players and console
    cooldown: 10 seconds
    cooldown message: Wait %remaining time% before greeting again.
    cooldown bypass: skript.greet.bypass
    cooldown storage: {greet_cooldown::%uuid of player%}
    trigger:
            send "Hello, %argument%" to the player
```

After writing your command, it's crucial to test it. Load your script into the server and try the command to ensure it works as expected. Pay attention to the syntax, permissions, and cooldown behavior.

Conclusion
Creating commands in Skript opens up a world of possibilities for customizing your Minecraft server. By understanding the command structure and carefully scripting the behavior, you can create powerful and useful commands that enhance the gameplay experience for you and your players. Remember to provide clear usage instructions and manage permissions appropriately to maintain a fun and secure environment. Happy scripting!

More Examples:
```js
command /broadcast <string>:
    usage: A command for broadcasting a message to all players.
    permission: skript.command.broadcast
    permission message: You dont have permission to broadcast messages
    aliases: /bc
    executable by: players and console
    cooldown: 15 seconds
    cooldown message: You last broadcast a message %elapsed time% ago. You can broadcast another message in %remaining time%.
    cooldown bypass: skript.command.broadcast.admin
    cooldown storage: {cooldown::%player%}
    trigger:
        broadcast the argument
```
