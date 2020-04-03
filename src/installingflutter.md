# Installing Flutter
## Android Studio
* Plug-ins -> Flutter
    * Installed Dart dependencies for you
* Restart Android Studio
* New "Create Flutter App" Options Shows up
* Create New Phone
    * Tools -> AVD Manager -> Create Virtual Device -> Pick Phone 
    * Got error `Emulator: PANIC: Cannot find AVD system path. Please define ANDROID_SDK_ROOT`
    * Accidentally deleted /home/[user]/Android/SDK file path. I thought it was not necessary.
    * Tools -> SKD Manager -> Android SDK -> Install SDK
    * To make sure it runs: 
        * Tools -> AVD Manger -> Click the Play button on the far right side of your emulator
        * Runs, but no Android :(. NO BIG DEAL, we just haven't started the app yet. 
        * Click Run (Shift+F10) and you should have an app running :)

### Thoughts
* Why start with Android Studio?
    * I am a big terminal boy. It is one centralized place to do everything you need at a lot less resource intensive state (not to mention much easier to configure), but learning to use it is always a steep learning curve. 
    * Cushion the blow by using an IDE first, then start moving down to the place that I like.
* Make it feel more like home (for now)
    * If you want to change the formatting style:
        * File -> Settings -> Editor -> Code Style -> Dart
        * Disable Dartfmt (first tab)
        * Change format how you want! 
    * Material Theme 
    * Vim Emulator

## Going Terminal
TODO: FINISH
