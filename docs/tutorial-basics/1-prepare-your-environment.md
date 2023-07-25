---
sidebar_label: 'Preparing Environment'
sidebar_position: 1
---

# Lets Prepare your Environment

Before starting up your new project with fairy, some prepare work is needed.

# JDK
Java Development Kit or JDK is a necessary part to build plugins/contributing on Fairy.

## Download
Before installing JDK uninstalling other JDKs are suggested, unless you understand what you are doing.

> If you are trying to contributing Fairy, JDK 8 will be necessary as Fairy should works from JDK 8 to latest (17). so Fairy itself shouldn't contain any high version functions or being compiled from high versions.

Both AdoptOpenJDK and Orcale's Offical JDK should works fine.
* [Oracle JDK 8](https://www.oracle.com/java/technologies/downloads/#java8)
* [AdoptOpenJDK JDK 8](https://adoptopenjdk.net/?variant=openjdk8&jvmVariant=hotspot)

# IDE and Plugins
Integrated Development Environment or IDE is recommended. We suggest to use [InteliJ IDEA](https://www.jetbrains.com/idea/download).

~~* [InteliJ Fairy Intergration](https://plugins.jetbrains.com/plugin/17197-fairy-integration)~~ (Deprecated 2022, please use https://github.com/FairyProject/fairy-bukkit-module-template until we find someone motivated enough to write the template xd)

We are not planning to make custom plugins for anything else than InteliJ. If you have any idea for custom plugins feel free to contact us or contributing to fairy.

# Gradle
Gradle is the JVM Build Tools that are used for Fairy itself and plugins/applications made on top of Fairy.

> You may have heard of Maven, it's also a JVM Build Tools. The reason we choose Gradle over Maven is because Gradle is a much more flexible build tools that allow us to made fairy even better.

To use Fairy to build your plugins/applications, you will need to use gradle on the project.

You can find a lot of documentation on [Gradle's Official Documentation](https://gradle.org/) including installation and more.