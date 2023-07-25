---
sidebar_label: 'Adding arguments (Basic)'
sidebar_position: 2
---

# Adding a parameter to your command

Alright, now that you've written your first command, you may want to add a parameter to it. Perhaps lets say you wish to say hello to someone in particular! 

Now, we would want our command to look like this:
```s
/testfairy <username>
```

And we would want the output to be:
```
[Fairy] Halo <username>!
```

In the fairy framework, this is *super* easy to add.

```java
@InjectableComponent
@Command(value = "testfairy", permissionNode = "fairy.test")
public class TestCommand extends BaseCommand {

    @Arg("name") 
    private String name

    @Override
    public void onHelp(CommandContext sctx) {
        sctx.sendMessage(MessageType.INFO, String.format("Halo %s!", name));
    }

}
```

As you can see, at the click of an annotation, you are capable of adding arguments, whether it be any of the following types:
- `Boolean`: Values accepted: "true", "on", "yes", "false", "off", "no"
- `Double`: Values accepted: Any double formatted "0.001" etc. NaN, Infinity and "E" values are rejected.
- `Float`: Values accepted: Any float formatted "0.001" etc. NaN, Infinity and "E" values are rejected.
- `Integer`: Values accepted: Any integer from `-2147483648` to `2147483647`
- `Long`: Values accepted: Any long formatted "10000000" from `-9223372036854775808` to `9223372036854775807`. NaN, Infinity and "E" values are rejected.
- `UUID`: Values accepted: Any valid UUID following the UUIDv4 format (8-4-4-4-12 for a total of 36 characters (32 hexadecimal characters and 4 hyphens). For example: `123e4567-e89b-12d3-a456-426614174000`.)
