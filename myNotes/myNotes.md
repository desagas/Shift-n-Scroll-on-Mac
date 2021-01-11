# Java/Minecraft Code Tricks

1.   `Minecraft.getInstance().currentScreen` has unlisted methods `hasShiftDown()`.
1.   IntelliJ, hover over Method/Package name, right click folder, click edit source --> allows you to view the code as shared under the license.
1.   `FMLClientSetupEvent` = clientSide tasks; `FMLServerStartingEvent` = serverSide tasks.
1.   There are Access Transformers for changing `final` modifiers in Minecraft code, amd Methods in java that can call on private methods, but also be used as a universal function/access method for all methods.
1.   MinecraftForge has Reflection build into its code, BUT, it ONLY works with Obf'd namespaces, it will not work with human-readable entries. Somewhere out there, there is a code that can tell you EXACTLY what the Obf'd namespaces are in any given class that you specify. I wanted to test it, but .git and my Mac, lets just say it got deleted. Easy to google, however.

# Unspoken Gradle for MacOS Tips
1. gradlew setup ***does not work on Mac,*** use ./gradlew setup.
1. Mods on Mac, load -> Gradle tab/fgruns/genIntelliJ.
1. Forge code editing, load -> gradlew setup -> Gradle tab/forge/tasks/genIntelliJ. Only edit in the project/forge directory, never the project/clean directory.