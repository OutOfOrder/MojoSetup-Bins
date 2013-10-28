MojoSetup Instructions
---------------

I'm using MojoSetup for the linux installer.. The installer binaries themselves are already pre-packaged in a "sh" install header (mojosetup.sh).  So all that is required is to simply put the game data and binaries in the right  folders beneath GameName.mojo and run the mojosetup-prepare script to build the installer.

Copying Files
--------------

Non architecture dependent Game data files go into the GameName.mojo/data/noarch folder.

The binaries and libraries go into the GameName.mojo/data/x86 or GameName.mojo/data/x86_64 depending on the architecture..  the structure is as follows..  (Libraries can be found in the 3rdParty folders) (assuming you use $ORIGIN/lib as your rpath

x86/
  GameName.bin.x86
  lib/libSDL2-2.0.so.0

the SDL2 lib needs to be the full SO with that name (e.g. libSDL2-2.0.so.0.0.0 renamed to libSDL2.2.0.so.0)  this is so we don't have to fiddle with symlinks (although mojo handles it perfectly..) (assuming you use $ORIGIN/lib64 as your rpath)

x86_64/
  GameName.bin.x86
  lib64/libSDL2-2.0.so.0

Configuring the installer
-------------------------

The main file that needs to be edited is the config.lua.  Here you can change the game name, executable name, and specify the sizes of the installed game. Read through the comments for basic settings to change..    For more advanced installers see the documentation in the source @ http://www.icculus.org/mojosetup/

Testing the Installer
---------------------

To test the installer use the bin/mojosetup-test script

./bin/mojosetup-test examples/GameName.mojo

This will launch the to test that your scripts etc.. are correct. 

*NOTE* when running in this mode installed executables will not have the execute bit set. They WILL have the correct execute bit when using the final ".zip" installer payload.

Building the Installer
----------------------
Once everything is "in-place".. it's time to build the installer..   

./bin/mojosetup-prepare examples/GameName.mojo GameName-Linux-1.0-2013-10-28.sh

it may ask you permission to remove a previous install.zip.. just say yes.

What this script does is package the contents of GameName.mojo into a zip file and then "append" the zip to the mojosetup.sh header.  and TADA, linux installer..

