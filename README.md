Geany for Mac OSX
=================

The files in this directory are used to create the Mac Application bundle
for Geany. Bundles contain all the dependencies, configuration, themes
and so on that are needed to run Geany.

Compilation guide
-----------------

Without repeating all kinds of documentation that is already available
elsewhere, the basic process is:

1. Download and run the `gtk-osx-build-setup.sh` script.  
    This prepares the jhbuild environment for building
2. Copy the `jhbuildrc-custom` to `~/.jhbuildrc-custom`, 
    over-writing the existing files.
3. Run jhbuild to get a OSX compatible GTK+ install with all needed
    dependencies. To do this, run these commands:  
    ```
    $ jhbuild bootstrap  
    $ jhbuild build meta-gtk-osx-bootstrap  
    $ jhbuild build meta-gtk-osx-core  
    ```
4. Download, compile and install the Murrine GTK+ engine into the
    jhbuild $PREFIX. This is optional, but allows for better themeing.
5. Download, compile and install the VTE library into the jhbuild 
    $PREFIX. This is optional, but allows for Terminal support in Geany.
6. Use jhbuild-shell to setup environment for building Geany.
7. Compile and install Geany into the jhbuild $PREFIX.
8. Download and install: `gtk-mac-bundler` 
9. Change to the `osx/` directory in Geany's source tree (this one this
    file is in) and run `gtk-mac-bundler geany.bundle` to create the application
    bundle.

Note: prepare to be frustrated ;)

Files details
-------------

Here's what the files in this directory do:

### Geany.icns

Geany's icons converted to Mac format. This format has the various icon
sizes all within one file.

### Info-geany.plist

Describes the app to the OS. Contains information like bundle name,
copyright and so on.

### geany.bundle

Settings file for gtk-mac-bundler to know how to create the application
bundle. This tells for example, which files to copy into the bundle.

### geany.conf

Default Geany configuration file for when one isn't in ~/.config/geany
already. This is a bit unusual but it allows to set some more appropriate
defaults for OSX.

### keybindings.conf

Default Geany keybindings to be more typical Mac keybindings, ex. where
the default for Save is Ctrl+s, this file changes that to Command+s.

### gtkrc

Customized GTK+ resource file to make Geany appear more appropriate on
OSX, like fonts, colours, etc. This theme is copied from the Greybird
theme used in Xubuntu (and elsewhere on Linux).

### jhbuildrc-custom

Config files for jhbuild to ensure the proper building.
  - These should be copied to ~/.jhbuildrc and ~/.jhbuildrc-custom before
    the first run of jhbuild so that it builds for the right architecture
    and so on.

### launcher.sh

Shell script copied into bundle that actually gets called first and
prepares the environment for running the real Geany binary. Anything
that needs to be done before running Geany can be done in here.

AUTHORS
------
- Matthew Brush (Original author) <matt(at)geany(dot)org>
- Trong-Thanh Tran <trongthanh(at)gmail(dot)com>