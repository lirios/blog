---
layout: post
title: "Liri Roadmap for 2017"
description: "Roadmap for 2017"
author: plfiorini
date: 2017-04-26 00:00:00 +0100
tags:
  - roadmap
---

**With 2017 already started and a few releases behind us, I want to provide an
insight about what we are currently working on and what the future holds.**

### Project management

With the help of the GitHub project management tools, we are now isolating
issues for the 1.0 release of several modules, in order to have a clear
vision of the next goals to tackle.

We also keep track of upstream issues that, in one way or another, have an
impact on our projects [here][upstream-issues].

### Priority to the toolkit

Fluid, our QtQuick toolkit, is a crucial part of the project for apps and the shell.

We want to implement missing features that were available from qml-material and
publish the documentation in a specific area of the Web site so developers will
have a reference and learn how to build apps for the platform.

We also expect to revamp its build system switching from cmake to qmake that has
better support from QtCreator.  
This will make Fluid easier to build on other platforms (no need to have cmake
and extra-cmake-modules around) and make Android deployment easier.

Material Design icons are going to be included along with the Fluid source code
without the need to launch a shell script for each build. This will result in
simpler development on every platform, especially on Windows where bash is not
always available. This also means that future source release tarballs will
be smaller.

**Fluid 1.0 is expected to be released in Q2 2017.**

Goals for future releases has already been set, as you can see from the GitHub
[milestones][fluid-milestones] page.

### Bundles

Another important feature we are working on are bundles for our apps.

Bundles put developers in control of how their apps are going to be built and
shipped to the users and allow them to get latest updates without waiting for
distribution to catch up.

They are also a much more efficient way of supporting multiple distributions
for us, because we can build only once and run everywhere.

#### Flatpak

One of our corner stones for the OS is to use bundles instead of traditional
packages, with Flatpak.

We recently announced the availability of the first experimental builds of the
Liri runtime and SDK as well as a few apps.

Flatpak made clear that some modules need to be split in smaller units.
This will allow us to release bits that are mature enough as 1.0, but are
currently part of larger repositories.

Liri runtime and SDK for Flatpak will have a stable release starting from
Fluid 1.0 in **Q2 2017**.

By then all apps are expected to be available via Flatpak.

#### Snap

While Flatpak is the preferred choice for the OS, we want to support Snap as well.
The first milestone has already been [completed][snap] and we now have a platform snap,
although it doesn’t include Qt Web Engine yet due to a build issue.

Apps are being snapped [here][snap-apps], there are Calculator and Text already.

A snap for the desktop environment was requested so if you know snap-fu your contribution
is welcome. Snap is the best way to bring the shell to Ubuntu, considering that it allows
much more control on Qt.

#### AppImage

Calculator, Text and Browser CI now produce AppImage bundles that we are testing out.

AppImage bundles for the cross-platform apps mentioned above will likely to be released
in **Q3 2017**. There are no plans to build the other apps at the moment.

### Apps

All apps are now using the new stack based on QtQuick Controls 2 and Fluid.

Text 0.2 was recently [released][text-release], Calculator 1.0 is around the corner
and Browser is progressing towards 1.0 with the help of Ivan Fateev, a new addition
to the team.

We want to focus on user experience first, polish the apps and have a stable release
before going into more complex features.

Cross-platform apps now have a nice icon made by Corbin Crutchley.

### Shell

QtWayland Compositor, one of the most important modules we rely on for the shell,
was finally released as stable with Qt 5.8.

Shortly after the xdg-shell v6 protocol for desktop-style user interfaces was released
and Gtk+ switched to it immediately. This broke Gtk+ apps on Liri OS that were previously
working. Once QtWayland Compositor support for xdg-shell v6 is complete we’ll be able
to run Gtk+ apps natively again.

Meanwhile the shell has been tested more and a lot of bugs were fixed. Since I’m happy
with the feature set I don’t plan to do more visible features before 1.0 and rather focus
on lower level features. The last feature I implemented is a better “present windows”
effect that combines Hawaii and Papyros features.

My Qt contributions are now shifting from QtWayland to eglfs, a Qt platform plugin for
running Qt apps on top of EGL and OpenGL ES 2.0 without an actual windowing system
like X11 or Wayland.

The shell is “just” a Qt app, with QtWayland Compositor and eglfs it implements a Wayland
windowing system that you can run on wide variety of targets like KMS or embedded platforms
such as Broadcom (Raspberry Pi), Vivante (Wandboard), Mali, etc…

The liri-wayland repository holds a fork of eglfs with more features such as logind
integration, screen hot plugging, resolution change, EDID parsing to get more screen
information, on the other hand eglfs progressed quite a lot in the past months and has
now support for NVIDIA binary blob.

The goal here is to upstream the changes in order to be able to use eglfs in the future
and leave the Qt folks with maintenance duties.

**The plan is to make the shell 1.0 available in late Q4 2017.**

[upstream-issues]: https://github.com/lirios/lirios/wiki/Upstream-Issues
[fluid-milestones]: https://github.com/lirios/fluid/milestones
[snap]: https://liri.io/blog/2017/03/17/introducing-platform-snap.html
[snap-apps]: https://github.com/lirios/snap-apps
[text-release]: https://liri.io/blog/2017/04/15/text-0.2.0.html