Available Runtimes
==================

This page provides information about available Flatpak runtimes. It is
primarily intended for application developers and distributors.

There are currently three main runtimes available: Freedesktop, GNOME, and
KDE. These are hosted on `Flathub <https://flathub.org/>`_. Each runtime comes
with a corresponding SDK for building and extensions for specific uses.

This section only offers a broad overview of the contents. To get up-to-date information, install the runtime and open a shell inside of
it (``flatpak run org.freedesktop.Sdk//23.08``). From there, you can look around or
use tools like ``pkg-config --list-all``. You can also inspect
``/usr/manifest.json``, which lists the sources used to build it.

Freedesktop
-----------

The Freedesktop runtime is the standard runtime that can be used for any
application. It includes a set of essential libraries and services, such as
D-Bus, GLib, Gtk3, PulseAudio, X11, and Wayland.

The Freedesktop runtime is maintained `here
<https://gitlab.com/freedesktop-sdk/freedesktop-sdk/>`__ and has a website
`here <https://freedesktop-sdk.io/>`__.

Available Freedesktop runtimes:

====================================================== =====================================
ID                                                     Description
====================================================== =====================================
org.freedesktop.Platform                               Runtime
org.freedesktop.Sdk                                    SDK
====================================================== =====================================

The following runtime extensions are available:

====================================================== =====================================
ID                                                     Description
====================================================== =====================================
org.freedesktop.Platform.Locale                        Runtime translations (extension)
org.freedesktop.Platform.VAAPI.Intel{,.i386}           Intel vaapi drivers (extension)
org.freedesktop.Platform.ffmpeg-full                   All ffmpeg codecs (extension)
org.freedesktop.Platform.Compat.{architecture}         32-bit compatible extension
org.freedesktop.Platform.Compat.{architecture}.debug   32-bit compatible extension (debug)
org.freedesktop.Platform.GL{,32}.default               Mesa drivers (extension)
org.freedesktop.Platform.GL{,32}.mesa-git              Mesa drivers, latest (extension)
org.freedesktop.Sdk.Debug                              SDK debug information (extension)
org.freedesktop.Sdk.Locale                             SDK translations (extension)
org.freedesktop.Sdk.Docs                               SDK documentation (extension)
org.freedesktop.Sdk.Extension.toolchain-{architecture} SDK cross compilers (extension)
====================================================== =====================================

GNOME
-----

The GNOME runtime is for applications that use the GNOME platform. Based
on the Freedesktop runtime, it adds the GNOME platform, which includes:

* Gjs
* GObject Introspection
* GStreamer
* GVFS
* Libnotify
* Libsecret
* LibSoup
* PyGObject
* Vala
* WebKitGTK

The GNOME runtime is maintained `here
<https://gitlab.gnome.org/GNOME/gnome-build-meta>`__.

Available GNOME runtimes:

=========================  =================================
ID                         Description
=========================  =================================
org.gnome.Platform         Runtime
org.gnome.Sdk              SDK
=========================  =================================

The following runtime extensions are available:

=========================  =================================
ID                         Description
=========================  =================================
org.gnome.Platform.Locale  Runtime translations (extension)
org.gnome.Sdk.Debug        SDK debug information (extension)
org.gnome.Sdk.Locale       SDK translations (extension)
org.gnome.Sdk.Docs         SDK documentation (extension)
=========================  =================================

KDE
---

The KDE runtime is for applications that use the KDE platform
or is Qt-based. Also based on the Freedesktop runtime, it adds Qt and KDE
Frameworks.

The KDE runtime is maintained `here
<https://invent.kde.org/packaging/flatpak-kde-runtime>`__.

Available KDE runtimes:

=======================  =================================
ID                       Description
=======================  =================================
org.kde.Platform         Runtime
org.kde.Sdk              SDK
=======================  =================================

The following runtime extensions are available:

=======================  =================================
ID                       Description
=======================  =================================
org.kde.Platform.Locale  Runtime translations (extension)
org.kde.Sdk.Debug        SDK debug information (extension)
org.kde.Sdk.Locale       SDK translations (extension)
org.kde.Sdk.Docs         SDK documentation (extension)
=======================  =================================

elementary
----------

The elementary runtime is for applications that wish to be published in
elementary AppCenter. Based on the GNOME runtime, it adds the elementary
platform, which includes:

* elementary Icons
* elementary Stylesheet
* elementary Sound Theme
* Granite

The elementary runtime is maintained `here
<https://github.com/elementary/flatpak-platform>`__.

Available elementary runtimes:

=============================  =================================
ID                             Description
=============================  =================================
io.elementary.Platform         Runtime
io.elementary.Sdk              SDK
=============================  =================================

The following runtime extensions are available:

=============================  =================================
ID                             Description
=============================  =================================
io.elementary.Platform.Locale  Runtime translations (extension)
io.elementary.Sdk.Debug        SDK debug information (extension)
io.elementary.Sdk.Locale       SDK translations (extension)
io.elementary.Sdk.Docs         SDK documentation (extension)
=============================  =================================
