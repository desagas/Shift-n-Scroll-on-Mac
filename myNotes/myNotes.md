# Java/Minecraft Code Tricks

1.   `Minecraft.getInstance().currentScreen` has unlisted methods `hasShiftDown()`.
1.   IntelliJ, hover over Method/Package name, right click folder, click edit source --> allows you to view the code as shared under the license.
1.   `FMLClientSetupEvent` = clientSide tasks; `FMLServerStartingEvent` = serverSide tasks.
1.   There are Access Transformers for changing `final` modifiers in Minecraft code, amd Methods in java that can call on private methods, but also be used as a universal function/access method for all methods.
1.   MinecraftForge has Reflection build into its code, BUT, it ONLY works with Obf'd namespaces, it will not work with human-readable entries. Somewhere out there, there is a code that can tell you EXACTLY what the Obf'd namespaces are in any given class that you specify. I wanted to test it, but .git and my Mac, lets just say it got deleted. Easy to google, however.
1.   When using [Access Transformers](https://mcforge.readthedocs.io/en/1.16.x/advanced/accesstransformers/), get it right, or you will have to reset your .gradle folder, which should be delete from time to time to remove caches and such, just take your jars out of the libs folder first. If you do it wrong, and your file becomes read only, just delete the file, reset your build.gradle to what it was before declaring the AT, and then refresh your gradle. And, remember, you can ONLY use Searge (obf) namespaces for fields and methods, while classes are as is.
1.   You can get the Searge (kind of obf'd, func_#/field_#/etc) names from build/fg_cache/mcp/[version-build]/joined/[long sequence of numbers]/rename/ by unarchiving output.jar, and comparing the Searge class file to the file accessed in #2 above.
1.   For mixin, you should set your Mixin_class with the same implements and same extends inorder to access all the functions that you may want to call. You can not call methods in your MixinClass from 

# Unspoken Gradle for MacOS Tips
1.   `gradlew setup` ***does not work on Mac,*** use `./gradlew setup.`
1.   Mods on Mac, load -> Gradle tab/fgruns/genIntelliJ.
1.   Forge code editing, load -> gradlew setup -> Gradle tab/forge/tasks/genIntelliJ. Only edit in the project/forge directory, never the project/clean directory.
1.   You can regularly delete the .gradle folder to rebuild the cache. Just make sure your internet conection is working before doing so, as it will download a new build once your gradle is refreshed.
