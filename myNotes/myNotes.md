# Java/Minecraft Code Tricks

1.   `Minecraft.getInstance().currentScreen` has unlisted methods `hasShiftDown()`.
1.   IntelliJ, hover over Method/Package name, right click folder, click edit source --> allows you to view the code as shared under the license.
1.   `FMLClientSetupEvent` = clientSide tasks; `FMLServerStartingEvent` = serverSide tasks.
1.   There are Access Transformers for changing `final` modifiers in Minecraft code, amd Methods in java that can call on private methods, but also be used as a universal function/access method for all methods.
1.   `git rm -r --cached .` so important. If you at one point or another change your .gitignore, this corrects, and makes your repo match the new one. You follow this up with `git add .` and `git commit`.

# Unspoken Gradle for MacOS Tips
1. gradlew setup ***does not work on Mac,*** use ./gradlew setup.
1. Mods on Mac, load -> Gradle tab/fgruns/genIntelliJ.
1. Forge code editing, load -> gradlew setup -> Gradle tab/forge/tasks/genIntelliJ. Only edit in the project/forge directory, never the project/clean directory.