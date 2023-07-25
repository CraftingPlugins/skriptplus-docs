---
sidebar_label: 'Your first command'
sidebar_position: 2
---

# Creating your first command

By default, you must extend the `BaseCommand`, as seen below

```java
@InjectableComponent
@Command(value = "testfairy", permissionNode = "fairy.test")
public class TestCommand extends BaseCommand {

    @Override
    public void onHelp(CommandContext sctx) {
        sctx.sendMessage(MessageType.INFO, "Halo!");
    }

}
```

First, lets deconstruct our annotations:
- `@InjectableComponent`: Typical annotation which will you find pretty much everywhere. This allows for the 
Fairy framework to inject your command
- `@Command`: This is what determines the typical info about your command, such as the name etc...
- `@CommandPresence`: Completely optional if you're going to make use of the CommandContext message
feature. This provides an interface which will link Fairy to whichever platform you're using.



```java
