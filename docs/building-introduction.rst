Building Introduction
=====================

:doc:`first-build` has already provided a quick demonstration of how
applications are built with Flatpak. This page provides an additional general
overview of what's involved.

flatpak-builder
---------------

``flatpak-builder`` is the primary tool for building Flatpak applications. It
allows you to take the source files for an application and build them into a
Flatpak package. It also allows multiple dependencies to be built
at the same time, which are then bundled into the final build.

The input to ``flatpak-builder`` is a manifest file. This file specifies
the parameters for the application to be built, including its name and
the runtime it will depend on. The manifest also lists all the modules
to be built as part of the build process. A source for each module can
be specified, including links to file archives or version control
repositories. One of the modules (usually the last one) is the application
code itself.

The basic format used to invoke ``flatpak-builder`` is::

 $ flatpak-builder <build-dir> <manifest>

Here, ``<build-dir>`` is the path to the directory where the application
will be built, and ``<manifest>`` is the path to the manifest file. The
contents of ``<build-dir>`` can be useful for testing and debugging purposes
but are generally treated as artifacts of the build process.

When ``flatpak-builder`` is run:

- The build directory is created if it doesn't already exist.
- The source code for each module is downloaded and verified.
- The source code for each module is built and installed.
- The build is finished by setting sandbox permissions.
- The build result is exported to a repository (which will be created
  if it doesn't already exist).

The application can then be installed from the repository and run.

Software Development Kits (SDKs)
--------------------------------

Instead of being built using the host environment, Flatpak applications are
built inside a separate environment called an SDK.

SDKs are similar to the regular runtime that applications run in; however,
SDKs also include all the development resources and tools required to
build an application. These resources include build and packaging tools,
header files, compilers, and debuggers.

Each runtime has a corresponding SDK. For example, there is both a GNOME
43 runtime and a GNOME 43 SDK. Applications that use the runtime are
built with the matching SDK.

Like runtimes, SDKs will sometimes be automatically installed for you.
However, if manual installation is necessary, they can be installed in
the same way as applications and runtimes, such as::

 $ flatpak install flathub org.gnome.Sdk//43
