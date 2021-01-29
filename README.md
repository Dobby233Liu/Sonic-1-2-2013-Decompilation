# Sonic 1/2 2013 Decompilation
This is a decompilation of RSDKv4, the engine used by the 2013 remakes of Sonic 1 & 2.

**Please support the original release of S1/S2 '13!**

# Obtaining the assets
Without assets from the remakes, this *game* won't run.
There is a [video tutorial](https://www.youtube.com/watch?v=gzIfRW91IxE) on how to obtain a legal `Data.rsdk` file.

You can get the remakes from:
  * [Sonic 1 (iOS, Via the App Store)](https://apps.apple.com/au/app/sonic-the-hedgehog-classic/id316050001)
  * [Sonic 2 (iOS, Via the App Store)](https://apps.apple.com/au/app/sonic-the-hedgehog-2-classic/id347415188)
  * [Sonic 1 (Android, Via Google Play)](https://play.google.com/store/apps/details?id=com.sega.sonic1px&hl=en_AU&gl=US)
  * [Sonic 2 (Android, Via Google Play)](https://play.google.com/store/apps/details?id=com.sega.sonic2.runner&hl=en_AU&gl=US)
  * [Sonic 1 (Android, Via Amazon)](https://www.amazon.com.au/Sega-of-America-Sonic-Hedgehog/dp/B00D74DVKM)
  * [Sonic 2 (Android, Via Amazon)](https://www.amazon.com.au/Sega-of-America-Sonic-Hedgehog/dp/B00HAPRVWS)

You don't need to be able to run them, you just need to extract the game assets from them.

For the Android version, please open the APK as a ZIP, open the `assets` folder, then copy the `Data.rsdk` file to the *game* folder.
If there is a `Data.rsdk.xmf` file instead, still copy it, then rename it to `Data.rsdk`.

# Transferring save file
If you want to transfer your save from the **Android pre-Forever versions**,
you can go to `*internal storage/SD card path*/Android/data/[game package name]/SGame.bin` and copy it to the *game* folder.

`[game package name]` can be:
  * `com.sega.sonic1` for Sonic 1
  * `com.sega.sonic2` for Sonic 2

# Additional Tweaks
* Added a built-in script compiler
* Added a `settings.ini` file that the game uses to load all settings, similar to Sonic Mania
* Dev menu can now be accessed from anywhere by pressing the `ESC` key if enabled in the config
* The debug pause key (F12), the step over & fast forward debug key (F11), and more debug features from Sonic Mania are all ported and are enabled with the dev menu
* If dev menu is enabled, pressing F10 will activate a palette overlay that shows the game's 8 internal palettes in real time

# TODOs:
- Add more native objects
- Add a proper HW rendering system
- Fix bugs
- Add CMake support
- Complete S2 networking code
  * We attempted to write code to handle the 2PVS mode in S2, but we couldn't finish for many reasons.
    We did leave our WIP code in the *game*, so if you think you could do it, give it a shot!

# How to build

## Windows

* Clone the repo
* Setup dependencies per the [depencencies README for Windows](./dependencies/windows/dependencies.txt)
* Build with the included Visual Studio solution

You can also grab a prebuilt executable from the Releases section.

## Windows via MSYS2 (64-bit only)

* Install the newest version of the MSYS2 by the installer from [here](https://www.msys2.org/) if you haven't.
* Launch the MINGW64 prompt (from the Start Menu/MSYS2 64-bit/MSYS2 MinGW 64-bit).
* Upgrade the system if you just installed it
  * Enter `pacman -Syuu` in the prompt and hit Enter.
  * Press `Y` when it asks if you want to update packages.
    * If it asks you to close the prompt, do so, then restart it and run the same command again.
* Install the dependencies with the following command:
  `pacman -S make git mingw-w64-i686-gcc mingw-w64-x86_64-gcc mingw-w64-x86_64-SDL2 mingw-w64-x86_64-libogg mingw-w64-x86_64-libvorbis`
* Clone the repo
* `cd` to the working tree (the repo's directory)
  * If you're not sure, run `ls` to check
* Run `make CXX=x86_64-w64-mingw32-g++ CXXFLAGS=-static -j4`
  * The `-j` switch is optional, but it will make building faster
    * The number parameter is based on the number of cores you have plus one, so 8 cores wold be -j9
    * If you don't want to calcuate, use `-j` without the parameter might be a choice (e.g. just `-j` instead of `-j[NUMBER]`)

## Windows UWP (Phone, Xbox, etc.)
* Clone the repo, then follow the instructions in the [depencencies readme for Windows](./dependencies/windows/dependencies.txt) and [depencencies readme for UWP](./dependencies/windows-uwp/dependencies.txt) to setup dependencies
* In the directory for the game you want to build, copy the `Data.rsdk` of it
  * `Sonic1Decomp.UWP` for Sonic 1
  * `Sonic2Decomp.UWP` for Sonic 2
  * or copy it's `Data.rsdk` file into `LocalState` of the *game* app later
* Build and deploy via `Sonic12Decomp.UWP.sln`
  * You may also need to generate visual assets
    * To do so, open the `Package.appxmanifest` file in the designer
    * Under the Visual Assets tab, select an image of your choice
    * Click Generate

## Linux
* To setup your build enviroment and library dependecies run the following commands:
  * Ubuntu/Debian (Mint, Pop!_OS, etc...): `sudo apt install build-essential git libsdl2-dev libvorbis-dev libogg-dev`
  * Arch Linux: `sudo pacman -S base-devel git sdl2 libvorbis libogg`
* Clone the repo
* `cd` to the working tree (the repo's directory)
  * If you're not sure, run `ls` to check
* Run `make -j4`
  * The `-j` switch is optional, but it will make building faster
    * The number parameter is based on the number of cores you have plus one, so 8 cores wold be -j9
    * If you don't want to calcuate, use `-j` without the parameter might be a choice (e.g. just `-j` instead of `-j[NUMBER]`)

## Mac:
* Clone the repo
* Follow the instructions in the [depencencies readme for Mac](./dependencies/mac/dependencies.txt) to setup dependencies
* Build via the XCode project

A Mac build of v1.0.0 by Sappharad can be found [here](https://github.com/Sappharad/Sonic-1-2-2013-Decompilation/releases/tag/1.0.0mac)

## Other platforms
Currently, the only supported platforms are the ones listed above.
However, the backend uses libogg, libvorbis & SDL2 to power it, so the codebase is basically multi-platform.

If you've cloned this repo and ported it to a platform not on the list, or made some changes you'd like to see added to this repo, submit a pull request and it'll most likely be merged.

There are also some unoffical ports:

### Vita
See [Xeeynamo's Vita branch](https://github.com/xeeynamo/Sonic-1-2-2013-Decompilation)

### Switch
See [heyjoeway's fork](https://github.com/heyjoeway/Sonic-1-2-2013-Decompilation)

# FAQ

* Q: The screen is tearing, how do I fix it?
A: Try turning on vsync. (Tested on Mac)

* Q: I found a bug/I have a feature request!
A: [Submit an issue](https://github.com/Rubberduckycooly/Sonic-1-2-2013-Decompilation/issues) and we'll try to fix/add it.

* Q: Did you have a decompilation of Sonic CD (2011)?
A: [Yes](https://github.com/Rubberduckycooly/Sonic-CD-11-Decompilation)!

* Q: Will you do a decompilation for Sonic Mania?
A: Maybe not. Sonic Mania is much bigger. Decompiling it not only need more knowledge on the far more complexier RSDKv5, it also need much more work (it has _600+_ objects!)

# Special Thanks
* [RMGRich](https://github.com/MGRich) for helping me fix bugs, tweaking my sloppy code and being helpful (it's fun to work with him) pronuns
* Everyone in the [Retro Engine Modding Server](https://dc.railgun.works/retroengine) for being supportive of me and for giving me a place to show off things that I discovered

# Contact
Please contact through the [Retro Engine Modding Discord Server](https://dc.railgun.works/retroengine) or [submit an issue](https://github.com/Rubberduckycooly/Sonic-1-2-2013-Decompilation/issues) for any extra questions.
