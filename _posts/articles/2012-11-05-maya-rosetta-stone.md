---
published: true
layout: article
title: Maya Rosetta Stone
abstract: A compendium of all known configuration otions for Autodesk Maya.
author_twitter: PaulNendick
author: Paul Nendick
categories:
- articles

---

# Who is this guide for?
Anyone who uses Autodesk Maya in anger, especially those of us doing so on Linux platforms. This list is a living work-in-progress. All details have been culled from official documentation, mailing lists, Autodesk support and the occasional reverse engineering. 

Many of these settings and better information can be gleaned by googling for [Autodesk's official docs](http://lmgtfy.com/?q=maya+2013+user+guide) but there are also quite a few items on this page not listed in any official documentation.

Please share any updates, addendums or corrections using the Feedback at the bottom of the page.

-Paul


# What can be done?
Maya provides to its users an enormous array of sporadically documented features and configuration options. These environment variables, XML config files and the like allow the user fine-grained control over:

* icons
* plug-ins
* modules
* Mel scripts
* Python scripts
* shaders
* image quality
* desktop integration
* tablet performance
* runtime stability
* more

# Prerequisites

* Maya 2011 or newer
* Linux, although much of this likely applies to Maya on Windows and OS X
* bash shell and not csh as the latter is [bad for you](http://www.faqs.org/faqs/unix-faq/shell/csh-whynot)

# Environment Variables
Following is a list of known Maya variables and what they configure. You can override these in your shell or embed them in [wrapper script](http://tldp.org/LDP/abs/html/wrapper.html).

## Personal options

### MAYA_APP_DIR
This variable defines your personal Maya application directory.

    export MAYA_APP_DIR=/opt/autodesk/maya/2013.5

### MAYA_UI_LANGUAGE
This is most useful when you want to run Maya in English on a Japanese version of Windows OS, i.e. never.

    export MAYA_UI_LANGUAGE=en_US
    export MAYA_UI_LANGUAGE=en_US/ja_JP

### AW_JPEG_Q_FACTOR
Alters the quality of jpegs written by Maya.

    export AW_JPEG_Q_FACTOR=95

## Performance options

### MAYA_NO_TBB
This issue is related to threading problem in the Maya Batch executable. Maya uses both TBB and OpenMP threading paths. When rendering we are seeing issues on the TBB side of the threading code were it seems to be calling too many thread counts and driving up the the systems ram causing and causing it to eventually crash almost instantly.

    export MAYA_NO_TBB=1
    
### MAYA_NO_PARALLEL_DRAW
If when using CGFX based shaders in a scene Maya crashes or freezes this will disable drawing of a shader which is still being evaluated.

    export MAYA_NO_PARALLEL_DRAW=1

### MAYA_NO_PARALLEL_MEMCPY
Set this environment variable to 1 to disable parallel memory copy. 

In some cases, parallel memory copy is faster on Opteron and Nehalem based systems. However, it may also be slower on Xeon systems, in which case you may want to disable parallel memory. If you are using Maya 2011 on Xeon system and are faced with speed issues, this might be useful.

    unset MAYA_NO_PARALLEL_MEMCPY
    
### MAYA_FORCE_REF_READ
By default, if you reference the same file twice, on file open Maya copies the existing nodes instead of re-reading them from disk. Occasionally, using this built-in multiple reference optimization feature of file referencing can cause errors. This environment variable turns off the file referencing optimization and forces reference files to be explicitly read in all cases. This fixes Maya’s behavior in some situations that would otherwise be evaluated incorrectly.

    unset MAYA_FORCE_REF_READ

### QT_PLUGIN_PATH
Disable KDE's Qt imageformat plugins as Maya does not need them and they make Maya's startup 4 times slower. If you want to use KDE's Qt image formats and are willing to accept the performance degradation, unset this variable.

    unset QT_PLUGIN_PATH

## Developer options
### XBMLANGPATH
The searth path(s) for icon files, such as those used for shelf buttons. Icons are in BMP or XPM format.

    export XBMLANGPATH=/somewhere/sensible:$XBMLANGPATH

### MAYA_SCRIPT_PATH
The search path(s) for shared MEL scripts.

    export MAYA_SCRIPT_PATH=/somewhere/sensible:$MAYA_SCRIPT_PATH


### MAYA_PLUG_IN_PATH
The search paths(s) for shared compiled plug-ins.

    export MAYA_PLUG_IN_PATH=/somewhere/sensible:$MAYA_PLUG_IN_PATH

### MAYA_MODULE_PATH
Defines the search paths for Maya module files. A module file describes the install location of a plugin which has been distributed as a module. Maya will append subdirectories of this install location to the following path variables: MAYA_PLUG_IN_PATH, MAYA_PRESET_PATH, MAYA_SCRIPT_PATH, PYTHONPATH and XBMLANGPATH. See [Distributing Maya Plug-ins() for more information](http://download.autodesk.com/us/maya/2010help/files/WS73099cc142f48755-4607e7cc11b1cfff5711f67.htm).

    export MAYA_MODULE_PATH=/somewhere/sensible:$MAYA_MODULE_PATH
    
### MAYA_PRESET_PATH
Location of Maya presets.

     export MAYA_PRESET_PATH=

### MAYA_PROJECTS_DIR
The default location of maya projects.

    export MAYA_PROJECTS_DIR=


### MAYA_PROJECT
Maya will allways start in this project.

    export MAYA_PROJECT=

### MAYA_MR_STARTUP_DIR
Location of the maya.rayrc startup file.

    export MAYA_MR_STARTUP_DIR=$MAYA_LOCATION/mentalray

### MI_CUSTOM_SHADER_PATH
Locations of mentalray include *.mi files.

    export MI_CUSTOM_SHADER_PATH=$MAYA_LOCATION/mentalray/include
    
## Debugging

### MAYA_CMD_FILE_OUTPUT
This feature is useful for tracking down error messages when Maya crashes upon startup.

    export MAYA_CMD_FILE_OUTPUT=$TMPDIR/maya.log

### WINEDITOR
Allows you to override the Expression Editor and use your own editor. The editor must be set to run in the foreground.

    export WINEDITOR=/usr/bin/scite

### MAYA_DEBUG_ENABLE_CRASH_REPORTING
Enable writing of crash report logs and dump files to temp directory. Crash report file example: `MayaCrashLog[yymmdd.hhmm].log`

    export MAYA_DEBUG_ENABLE_CRASH_REPORTING=1

### MAYA_HBDOWN_DEBUG
Enable verbose logging of hotbox actions for debugging issues on Linux. Slows Maya considerably.

    export MAYA_HBDOWN_DEBUG=1
    
## Installation options
### MAYA_VERSION

This is a Baseblack invention making it ~easy~ possible to install multiple versions of Maya simultaneously.

    export MAYA_VERSION=default




    