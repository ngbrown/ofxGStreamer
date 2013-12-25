ofxGStreamer
============

openFrameworks addon to use gstreamer under osx and windows. This addon has no code and instead uses the addon_config.mk file to add the needed files from the core + the flags needed to compile using gstreamer

This will only work with the latest version of the project generator from github (10/10/2013)

##Installing gstreamer

###osx

For osx, this addon depends on the gstreamer SDK. To install it:

You can download gstreamer v1.0. To install it under osx use the packages from [http://gstreamer.freedesktop.org/data/pkg/osx/1.2.1/](http://gstreamer.freedesktop.org/data/pkg/osx/1.2.1/)
    
* [gstreamer-1.0-1.0.8-universal.pkg](http://gstreamer.freedesktop.org/data/pkg/osx/1.2.1/gstreamer-1.0-1.2.1-universal.pkg "gstreamer-1.0-1.2.1-universal.pkg") installs the necesary libraries for applications to run

* [gstreamer-1.0-devel-1.0.8-universal.pkg](http://gstreamer.freedesktop.org/data/pkg/osx/1.2.1/gstreamer-1.0-devel-1.2.1-universal.pkg "gstreamer-1.0-devel-1.2.1-universal.pkg") installs the development files needed to compile gst aplications

* [gstreamer-1.0-1.0.8-universal-packages.dmg](http://gstreamer.freedesktop.org/data/pkg/osx/1.2.1/gstreamer-1.0-1.2.1-universal-packages.dmg "gstreamer-1.0-1.2.1-universal-packages.dmg") contains some additional packages that are needed to encode some formats like h264, some of this packages have GPL license or use patented formats. From those this package is needed to do colorspace conversion:

    * gstreamer-1.0-libav-1.0.8-universal.pkg

    * And these will provide h264 encoding and some network utils to stream h264 and other formats:
      * gstreamer-1.0-codecs-restricted-1.0.8-universal.pkg
      * gstreamer-1.0-net-restricted-1.0.8-universal.pkg

If we only want to run an osx app. The devel package is not needed but by now we need to install the rest of packages

On some systems it seems it's necesary to remove or rename /Library/Frameworks/GStreamer/Headers/assert.h or it'll clash with the assert.h in the system and some projects won't compile. As far as i've tested it's safe to just delete it but it's probably better to keep a copy just in case.

###Windows (Visual Studio)

For Windows, this addon includes enough of the gstreamer SDK to compile and only depends on the gstreamer redistributable being installed.

To install gstreamer v1.0 under Windows, download the installer from [http://gstreamer.freedesktop.org/data/pkg/windows/1.2.1/](http://gstreamer.freedesktop.org/data/pkg/windows/1.2.1/)

The following are the basic steps:

1. [http://gstreamer.freedesktop.org/data/pkg/windows/1.2.1/gstreamer-1.0-x86-1.2.1.msi](http://gstreamer.freedesktop.org/data/pkg/windows/1.2.1/gstreamer-1.0-x86-1.2.1.msi "gstreamer-1.0-x86-1.2.1.msi") installs the necessary libraries for applications to run.  Use the "Custom" option for complete control over what codecs are installed.
2. After MSI installation, set environment variables.
	* Add the `.\bin` directory to the system environment `path` variable.
	* Set the `.\lib\gstreamer-1.0` path to the `GST_PLUGIN_SYSTEM_PATH_1_0` variable.

You may want to install the full SDK for more advanced use of gstreamer.

##Use in application code
In the example application, only two lines were added from the OpenFramework `videoPlayerExample` application code.

After constructing the `ofVideoPlayer` class and before loading or playing a video, use the `setPlayer` function to select the `ofGstVideoPlayer`.

1. Include the appropriate header:

		#include "ofGstVideoPlayer.h"

2. Set the player in the `setup()` function:

		fingerMovie.setPlayer(ofPtr<ofGstVideoPlayer>(new ofGstVideoPlayer));

If you don't do this, `ofVideoPlayer` will default to QuickTime in Windows and QuickTime (pre 10.7) or QTKit in OSX.