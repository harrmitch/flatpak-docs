Dependencies
============

Flatpak provides a number of options for how applications can depend
on other softwares. When setting out to build an application with Flatpak
for the first time, it is therefore necessary to decide how application
dependencies will be organized.

This page outlines the available options and provides guidance on
when to use each one.

Runtimes
--------

As described in :doc:`basic-concepts`, runtimes provide basic
dependencies that applications can use, as well as the environment
in which applications run. Flatpak requires each application to
specify a runtime. Therefore, one of the first decisions you need to make
when building an application with Flatpak is which runtime it will use.

An overview of the available runtimes can be found on the
:doc:`available-runtimes` page. There are deliberately only a small number
of runtimes to choose from. Typically, runtimes are selected
based on the dependencies required by an application. If a runtime
exists that provides the libraries you plan to use, this is usually
the correct runtime to choose.

.. tip::

  Runtimes require regular maintenance, and application developers should
  generally avoid creating their own.

Runtimes are automatically installed for users when they install an
application, and build tools can also automatically install them for
you (``flatpak-builder``'s ``--install-deps-from`` option is useful for
this). However, if you do need to manually install your chosen runtime,
you can do so in the same way as installing an application, using the
``flatpak install`` command. For example, the command to install the GNOME
43 runtime is::

  $ flatpak install flathub org.gnome.Platform//43

Bundling
--------

One of the key advantages of Flatpak is that it allows application
authors to bundle any libraries or dependencies they want. This
means that developers aren't limited to only the libraries offered by
Linux distributions.

When building an application for the first time, you will need
to decide which dependencies to bundle. This can include:

- libraries that aren't in your chosen runtime
- different versions of libraries that are in your chosen runtime
- patched versions of libraries
- data or other resources that are part of the application

As will be seen, bundled dependencies can be automatically downloaded as
part of the build process. It is also possible to apply patches and perform
other transformations.

While bundling is very powerful and flexible, it also places a greater
maintenance burden on the application developer. Therefore, while it is
possible to bundle as many modules as you like, it is generally recommended
to keep the number of bundled modules as low as possible. If a dependency
is available as part of a runtime, it is generally better to use that version
rather than bundle it yourself.

The specifics of how to bundle libraries are covered in the :doc:`manifests`
section.

BaseApps
--------

Runtimes and bundling are the two main ways in which dependencies are handled
with Flatpak. They allow applications to rely on stable collections of
dependencies while also providing flexibility and control.

However, in some cases, dependencies come as part of a bigger framework or
toolkit, which doesn't fit into a runtime but which is also cumbersome to
manually bundle as a series of individual modules. This is where *BaseApps*
come in.

BaseApps contain collections of bundled dependencies which can then be
bundled as part of an application. They don't get rebuilt as part of the
build process, which makes building faster (particularly when bundling large
dependencies). And because each BaseApp is built only once, it is guaranteed
to be identical wherever it is used, meaning that it is saved only once on disk.

BaseApps are a relatively specialized concept, and only some applications
need to use them (the most common BaseApp is used for `Electron applications
<https://github.com/flathub/io.atom.electron.BaseApp>`_). However, if your
application uses a large, complex, or specialized framework, it is a good
idea to check for available BaseApps before you start building.

Extensions
----------

Runtimes and applications can define extension points which allow optional
additional runtimes to be mounted at specified locations inside the sandbox
when they are present on the system. Typical uses for extensions include
translations for applications, debuginfo for sdks, or adding more functionalities
to the application. Some softwares refer to these extensions as "Add-ons".

For an extension to be loaded in the application or runtime, an extension
point must first be defined in the application or runtime in 
question.

By convention, extension points follow the ID of the application or
runtime, followed by a generic term for the extension.
For example, the OBS Studio flatpak may define the extension point
``com.obsproject.Studio.Plugin``, where "Plugin" is the generic term
prefixed by the application ID.

To see available extension points, it is best to look at the
manifest of the application or runtime.

Now, any extension that chooses to be loaded inside the OBS Studio flatpak
must prefix its ID with ``com.obsproject.Studio.Plugin``, such as
``com.obsproject.Studio.Plugin.Gstreamer``, for example.

Some extension names have special significance, as discussed below.

- ``.Debug`` is used for Debug extensions by applications, runtimes,
  and SDKs. These extensions are used for debugging purposes. Every application
  or runtime built with ``flatpak-builder`` produces a ``.Debug``
  extension unless specifically disabled in the manifest.

  A ``.Debug`` extension is necessary for generating useful
  backtraces, as further explained in :doc:`debugging`.

- ``.Locale`` is used for Locale extensions by applications or
  runtimes. These extensions add support for additional languages to
  the parent application or runtime. They are usually partially
  downloaded by ``flatpak`` based on the configured system locale.
  Every application or runtime built with ``flatpak-builder`` produces
  a ``.Locale`` extension unless specifically disabled in the
  manifest.

- ``.Sources`` is used for Sources extensions by applications or
  runtimes. These extensions bundle the source code of the modules
  used in the application or runtime. ``flatpak-builder`` will
  produce a ``.Sources`` extension prefixed by the ID when
  ``--bundle-sources`` is used.

Please visit :doc:`extension` for a guide on how to create 
extension points and extensions.
