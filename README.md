This documentation was last updated for Liferea version 1.11 (02.06.2014).

Contents
========

   1. ............. Introduction

   2. ............. Installing from Package

   3. ............. Compiling Liferea Yourself
   3.1. ............. Dependencies
   3.2. ............. Compiling From Tarball
   3.3. ............. Compiling From Git

   4. ............. Contributing
   4.1. ............. No Feature Requests!
   4.2. ............. How to Provide Patches
   4.3. ............. How to Translate Liferea
   4.3.1 .............. Create a New Translation
   4.3.2 .............. Update an Existing Translation
   4.3.3 .............. Provide a Localized Feed List
   4.4. ............. How to Create Plugins
   4.4.1. ............. Why We Use Plugins
   4.4.2. ............. How to Interact With Liferea
   4.4.3. ............. Testing Plugins
   4.5. ............. How to Help With Testing
   4.5.1. ............. Bug Reports
   4.5.2. ............. Debugging Crashes
   4.5.3. ............. Debugging Memory Leaks
   
   5. ............. Browser Integration

   6. ............. How to Get Support


1. Introduction
===============

Liferea is an abbreviation for Linux Feed Reader. It is a news aggregator for 
online news feeds. It supports a number of different feed formats including 
RSS/RDF, CDF and Atom. There are many other news readers available, but these 
others are not available for Linux or require many extra libraries to be 
installed. Liferea tries to fill this gap by creating a fast, easy to use, 
easy to install news aggregator for GTK/GNOME.



2. Installation from Package
============================

Detailed instructions on how to install Liferea on the different distributions can 
be found online on our homepage at

	http://lzone.de/liferea/install.htm



3. Building Liferea Yourself
============================

This section describes how to compile Liferea yourself. If you have
any problems compiling the packages or from GIT don't hesitate to
contact us in IRC (see Support section) to help you with it!


3.1 Dependencies
----------------

Liferea 1.11+ is to be built against GTK+ 3. If you need to build
for GTK+ 2 please use the most recent 1.8 release.

The compilation and runtime dependencies are:

Mandatory:

   gtk3
   libxml2
   libxslt
   sqlite3
   libwebkit3
   libjson-glib
   libgirepository1.0
   libpeas
   gsettings-desktop-schemas

Optional:

   -> For the keyring support
        Python >= 2

   -> For the media player plugin
	Python >= 2
        GStreamer 0.10+ library and codecs
   
Ensure that you have installed the libraries and their headers.
If you use distribution packages then you usually need to install
a package named like the library and one with a suffix "-dev" or
"-devel". You need both to compile Liferea.


3.2 Compiling from Tarball
--------------------------
		
If you do not like version control systems you might want to compile
Liferea from a release tarball. Those are supplied at our SourceForge
project homepage (http://lzone.de/liferea). After you downloaded it 
extract it like this:

   tar jxvf liferea-1.11.0.tar.bz2 

After unpacking run the standard autotools commands:

   ./configure
   make
   make install
   
After this Liferea will be installed in /usr/local and you should be
able to start it by calling "/usr/local/bin/liferea".


3.3 Compiling from Git
----------------------

To anonymously check out a source copy execute this:

   git clone https://github.com/lwindolf/liferea.git

Then build it with:

   ./autogen.sh
   make
   make install


4. Contributing
===============

This section describes how you can contribute to Liferea. We currently
try to provide additional help on contributing via OpenHatch.org which
provides help and easy tasks to start contributing.

	http://openhatch.org/+projects/Liferea

As the project is hosted at Github pull requests and tickets via Github
are the best way to contribute to Liferea.


4.1. No Feature Requests!
-------------------------

First: *Feature requests are no contributions*. A lot of users think so and
don't see at all why this should not be the case. While there might be a
bit of interest on what new features the users would like to have, feature
requests tend to take up *a lot* of the time spent on support. Short of 
ignoring feature requests the only polite way to answer them is an elaborate
explanation of the reason why the developers have decided not to implement
this feature requests and that they already have thought about it. So feature
requests are a constant justification exercise invented to punish developers.
Please be kind and do not participate in this.


4.2. How to Provide Patches
---------------------------

Here are some rules to supply patches:

1.) Before spending time on your topic announce it first on the mailing
    list or the IRC channel. This avoids duplicate work and ensures your
    patch will be accepted.
    
2.) Try to be close to our coding style.

3.) Please include a ChangeLog entry in your patch.

4.) If possible provide the patch as a Github pull request. If you are
    not familiar with pull requests post the patch in the mailing list.
    In such a case please always specify for which release or commit id
    you created the patch. 

If you are working on some topic feel free to contact us with any question
on the mailing list on the IRC channel (see Support section).


4.3. How to Translate Liferea
-----------------------------

Before starting to translate you need a translation editor. We suggest
to use poedit or gtranslator. Please edit the translation using such a 
translation editor and send us the resulting file. Once you have finished
your work please send us the resulting file.

Please do not send translation patches. Those are a lot of work to merge
and the bandwidth saving is not that huge!


4.3.1. Create a New Translation
-------------------------------

To create a new translation you must load the translation template, which you
can find in the release tarball as "po/liferea.pot", into the translation 
editor. After editing it save it under a new name (usually your locales name
with the extension ".po").


4.3.2. Update an Existing Translation
--------------------------------------

When updating an existing translation please ensure to respect earlier 
translators work. If the latest translation is only a few months old please
contact the latest translator first asking him to review your changes especially
if you change already translated literals.


4.3.3. Providing a Localized Feed List
--------------------------------------

When Liferea starts for the first time it installs a localized feed list
if available. If this is not the case for your locale you might want to provide
one. To check if there is one for your country have a look into the "opml"
subdirectory in the latest release tarball or GIT.

If you want to provide/update a localized feed list please follow these rules:

1.) Keep the English part of the default feed list

2.) Only add neutral content feeds (no sex, no ideologic politics, no illegal stuff)

3.) Provide good and short feed titles

4.) Provide HTML URLs for each feed.

Once finished post the result OPML file in the mailing list or the SF patch
tracker.


4.4 How to Create Plugins
-------------------------

Liferea 1.10+ support GObject Introspection based plugins using libpeas. The
Liferea distribution comes with a set of Python plugin e.g. the media player,
GNOME keyring support, a tray icon plugin and maybe others.


4.4.1. Why We Use Plugins
-------------------------

The idea behind plugins is to extend Liferea without changing compile time
requirements. With the plugin only activating if all its bindings are available
Liferea uses plugins to automatically enable features where possible.


4.4.2. How to Interact With Liferea
-----------------------------------

You can develop plugins for your private use or contribute them upstream.
In any case it makes sense to start by cloning one of the existing plugins
and to think about how to hook into Liferea. There are two common ways:

   1.) using interfaces,
   2.) or by listening to events on Liferea objects,
   3.) or not at all by just controlling Liferea from the outside.

The media player is an example for 1.) while the tray icon is an example for 3.)
If you find you need a new plugin interface (called Activatables) in the code 
feel free to contact us on the mailing list. In general such a tight coupling
should be avoided.

About the exposed GIR API: At the moment there is no stable API. Its just some
header files fed into g-ir-scanner. Despite this method names of the core
functionality in Liferea has proven to be stable during release branches. And
if you contribute your plugin upstream it will be updated to match renamed
functionality.


4.4.3. Testing Plugins
----------------------

To test your new plugin you can use ~/.local/share/liferea/plugins. Create 
the directory and put the plugin script and the .plugin file there and restart
Liferea.

Watch out for initialization exceptions on the command line as they will
permanently disable the plugin. Each time this happens you need to reenable
the plugin from within the plugin tab in the preferences dialog!


4.5 How to Help With Testing
----------------------------

4.5.1. Bug Reports
------------------

If you want to help with testing grab the latest tarball or follow GIT master
and write bug reports for any functional problem you experience. If you have
time help with bug triaging the SF tracker. Check if you see any of the open
bugs on your setup.


4.5.2. Debugging Crashes
------------------------

In case of crashes create gdb backtraces and post them in the bug tracker. To
create a backtrace start Liferea using "gdb liferea". At the gdb prompt type
"run" to start the execution and "bt" after the crash. Send us the "bt" output!

Note: Often people confuses assertions with crashes. Assertions do halt the
program because of a totally unexpected situation. Creating a backtrace in this
situation will only point to the assertion line, which doesn't help much. In case
of an assertion simply post a bug report with the assertion message.


4.5.3. Debugging Memory Leakage
-------------------------------

If you see memory leakage please take the time to do a run 

   "valgrind --leak-check=full liferea"

to identify leaks and send in the output.


5. Browser Integration
======================

Liferea allows subscribing directly from Firefox 2.0+ and Epiphany. 

5.1. Ephiphany
--------------

Epiphany provides a standard plugin that allows adding subscription directly 
to Liferea. Ensure you have installed the Epiphany plugins (often a separate
package in the distribution) and enabled the plugin in the Epiphany settings.

5.2. Firefox 2.0+
-----------------

If you want to subscribe from within Firefox 2.0 you can configure Firefox 2.0 
to add subscriptions to Liferea directly. To do so click the feed icon in the 
location  entry. Firefox will then present a menu where you can configure a 
manual command instead of the Live Bookmarks to add subscriptions. Liferea 
supplies a script named "liferea-add-feed" that you can tell Firefox to use.

If this doesn't work for you please try to run "liferea-add-feed" from the
command line and look for error messages. Often DBUS problems cause the script
to fail.


6. How to Get Support
=====================

When using distribution packages:

   Do not post bug reports in the Liferea bug tracker, use the bug reporting
   system of your distribution instead. We (upstream) cannot fix distribution
   packages!

Before getting support for stable releases: 

   Install the latest stable release and check if the problem is solved already. 
   Please do not ask for help for older releases!

Now there are three major support channels:

1.) The IRC channel "#liferea" on freenode.org. If you have easy to solve 
    problems and simple questions feel free to ask the people hanging 
    around there.
    
2.) The mailing list. Good for posting compilation problems and starting
    longer discussions.
    
3.) The SourceForge bug tracker (http://sf.net/projects/liferea) where you
    can post bug reports for all problems you find. Ensure to look for any
    existing reports on your problem!

Hopefully we can help with your problem.