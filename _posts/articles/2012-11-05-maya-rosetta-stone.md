---
published: false
layout: article
title: Your Post Title
abstract: Short summary of your article.
author_twitter: PaulNendick
author: Paul Nendick
categories:
- articles

---

# Who is this guide for?
Anyone who uses Autodesk Maya in anger, especially those of us doing so on Linux platforms.


# What can be done?
Maya provides to its users an enormous array of sporadically documented features and configuration options. These environment variables, XML config files and the like allow the user fine-grained control over:

* icons
* plug-ins
* modules
* Mel scripts
* Python scripts
* shaders
* stability of Maya itself
* more

# Prerequisites

* Maya 2011 or newer
* Linux, although much of this likely applies to Maya on Windows and OS X
* bash shell and not csh as the latter is [bad for you](http://www.faqs.org/faqs/unix-faq/shell/csh-whynot)

# Environment Variables
Following is a list of known Maya variables and what they configure. You can override these in your shell or embed them in wrapper script.

## Personal options

### MAYA_APP_DIR
This variable defines your personal Maya application directory.

    export MAYA_APP_DIR=$HOME/maya

### MAYA_UI_LANGUAGE
This is most useful when you want to run Maya in English on a Japanese version of Windows OS, i.e. never.

    export MAYA_UI_LANGUAGE=en_US
    export MAYA_UI_LANGUAGE=en_US/ja_JP

