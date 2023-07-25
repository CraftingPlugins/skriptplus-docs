---
sidebar_label: 'Adding arguments (Advanced)'
sidebar_position: 2
---

# Adding a custom parameter to your command

Alright, now that you've written your first command, you may want to add an advanced parameter to it. Perhaps lets say you wish to say hello to someone in particular! 

Now, we would want our command to look like this:
```s
/finduser <username>
```

And we would want the output to be:
```
[Fairy] Halo <username>, you have <coins> coins!
```

In the fairy framework, this is *super* easy to add.

Writing your own custom argument may be crucial at times. What if you wanted the user to specify the username of another user! You could, as opposed to writing a user query every single time in your command, just create a custom argument processor for the class "Player".

Lets say we have the following service:
```java
@Service
public class UserService {
    private final Map<String, User> users = new HashMap<>();

    public void addUser(final User user) {
        users.put(user.getName(), user);
    }

    public User getUser(final String name) {
        return users.get(name);
    }

    public List<String> getMatching(final String name) {
        // Performance go brrr
        return users.keySet()
                .stream()
                .filter(e -> e.contains(name))
                .collect(Collectors.toList());
}
```
```java
public class User {
    private final String name;
    private int coins;

    public User(final String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public int getCoins() {
        return coins;
    }
}
```

If you've previously missed the last tutorial on the basics of commands, we highly advise you go read it [here](2-adding-parameters). Following the same principles of the last tutorial, we would typically have for a command the following:

## The wrong way 💩

```java 
@InjectableComponent
@Command(value = "finduser", permissionNode = "fairy.test")
@CommandPresence(DefaultPresenceProvider.class)
public class TestCommand extends BaseCommand {

    @Arg("name")
    private String name
💩
    @Autowired💩
    private UserService userService;

    @Override
    public void onHelp(CommandContext sctx) {
        final User user = userService.getUser(name);

        if (user == null) {
            sctx.sendMessage(MessageType.ERROR, String.format("Could not find user of name %s!", user.getName()));
            return;
        }

        sctx.sendMessage(MessageType.INFO, String.format("Halo %s!", user.getName()));
    }
}
```

But this is **boring**. If we're having to add null checks and user conversion in *every single method*, it's going to get annoying *very* fast. And as the programming paradigm reminds us, "DRY" (Don't Repeat Yourself). 

## The right way 😎

Lets create an Arg transformer to handle this in an automated fashion.

```java
@InjectableComponent
public class UserArgTransformer implements ArgTransformer<User> {

    // Cute dependency injection
    @Autowired
    private UserService userService;

    /**
     * This is the array of classes this support.
     * You can add all subclasses too if they share
     * a common superparent. 
     */ 
    @Override
    public Class[] type() {
        return new Class[]{User.class};
    }

    /**
     * This is what parses the argument from a "String"
     * to the object you specify.
     */ 
    @Override
    public User transform(CommandContext commandContext, String s) throws ArgTransformException {
        final User user = userService.getUser(s);

        if (user == null) {
            // Failure will cause an internal exception.
            // No need for returns here.
            this.fail("User does not exist");
        }
        return user;
    }

    /**
     * This is to support Tab completion, most
     * often used on Minecraft and CLI apps
     */
    @Override
    public List<String> tabComplete(CommandContext commandContext, String source) throws ArgTransformException {
        return userService.getMatching(source);
    }
}
```

With this argument transformer, whenever `@Arg` preceeds a `User` object, it will pass the String into the ArgTransformer, which will successfully (or unsuccesfully!) parse it. we can effectively do
the following:

```java
@InjectableComponent
@Command(value = "finduser", permissionNode = "fairy.test")
@CommandPresence(DefaultPresenceProvider.class)
public class TestCommand extends BaseCommand {

    @Arg("user")
    private User user

    @Override
    public void onHelp(CommandContext sctx) {
        sctx.sendMessage(MessageType.INFO, String.format("Halo %s! You have %d coins!", user.getName(), user.getCoins()));
    }
}
```

Pretty cool right! Now that we've automated the parsing, you may use as many custom arguments; Heck, you may even create behaviours if a user uses a particular attribute!