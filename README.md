Ouzel v0.40
Build Status Build Status Quality Gate Join the chat at https://gitter.im/ouzelengine/Lobby
by elnormous and KogeDeveloper
Ouzel is a C++ game engine mainly targeted for development of 2D games.

Supported platforms:

Windows 7, 8, 10
macOS 10.8+
Linux
iOS 8+
tvOS 9+
Android 3.0+
Emscripten (sample)
Supported rendering backends:

Direct3D 11
OpenGL 2, OpenGL 3 and OpenGL 4
OpenGL ES 2 and OpenGL ES 3
Metal
Supported audio backends:

XAudio 2
DirectSound
CoreAudio
OpenAL
OpenSL ES
ALSA
Features
Cross-platform (Windows, macOS, iOS, tvOS, Android, Linux, and Emscripten targets supported)
Multi-threaded (separate threads for rendering, sound, and game)
2D and 3D scene management
GUI helper classes and management
Bitmap and true-type font support
Multiple side-by-side viewport support
XInput, DirectInput, IOKit, Apple GameController, and Linux evdev gamepad support
Actor animation (including tweening) system
Particle systems
Resource caching system
Localization support via loading string translations and UTF-8 string support
Software audio mixer for sound effect playback
High DPI support on Windows, macOS, and iOS
Easy to install (just pull the repository and it's subrepositories and build it)
Example app
The following code will open create a scene with a sprite in the center of it:

#include "ouzel.hpp"

class Example: public ouzel::Application
{
public:
    Example():
        assets(ouzel::engine->getCache())
    {
        assets->loadAsset(ouzel::assets::Loader::IMAGE, "player.png");
        ouzel::engine->getSceneManager().setScene(&scene);
        scene.addLayer(&layer);
        cameraActor.addComponent(&camera);
        layer.addChild(&cameraActor);
        playerSprite.init("player.png");
        player.addComponent(&playerSprite);
        layer.addChild(&player);
    }

private:
    ouzel::scene::Scene scene;
    ouzel::scene::Layer layer;
    ouzel::scene::Camera camera;
    ouzel::scene::Actor cameraActor;
    ouzel::scene::Sprite playerSprite;
    ouzel::scene::Actor player;
    ouzel::assets::Bundle assets;
}

std::unique_ptr<ouzel::Application> ouzel::main(const std::vector<std::string>& args)
{
    return std::unique_ptr<ouzel::Application>(new Example());
}

Compilation
GNU makefile, Xcode project, and Visual Studio project files are located in the "build" directory. Makefile and project files for sample project are located in the "samples" directory.

You will need to download OpenGL (e.g. Mesa), ALSA, and OpenAL drivers installed in order to build Ouzel on Linux. For x86 Linux also libx11, libxcursor, libxi, and libxss are required.

To build Ouzel with Emscripten, pass "PLATFORM=emscripten" to "make" command, but make sure that you have Emscripten SDK installed before doing so:

$ make PLATFORM=emscripten
You can build Android samples and run them on an Android device by executing the following commands in "samples/android" directory (Android SDK and NDK must be installed and added to PATH):

$ gradle assembleDebug
$ gradle installDebug
$ adb shell am start -n org.ouzel/org.ouzel.MainActivity
Because on Raspbian Stretch libEGL.so was renamed to libbrcmEGL.so and libGLESv2.so to libbrcmGLESv2.so you will have to run the following commands before building the samples on Raspbian 8 (Jessie) or older:

$ sudo ln -s /opt/vc/lib/libEGL.so /opt/vc/lib/libbrcmEGL.so 
$ sudo ln -s /opt/vc/lib/libGLESv2.so /opt/vc/lib/libbrcmGLESv2.so
System requirements
Windows 7+ with Visual Studio 2015 or Visual Studio 2017
macOS 10.10+ with Xcode 7.2+
Any reasonable new Linux distro (x86 and ARM are supported)
Getting help
You can ask question in the following locations:

Author of the Ouzel engine: https://twitter.com/elnormous Teogether with https://twitter.com/KogeDeveloper
Development roadmap: https://trello.com/b/5tRlUXKR/ouzel-roadmap
License
Ouzel codebase is licensed under the BSD license. Please refer to the LICENSE file for detailed information.
