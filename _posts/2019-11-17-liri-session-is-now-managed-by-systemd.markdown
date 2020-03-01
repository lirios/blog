---
layout: post
title: "Liri session is now managed by systemd"
description: ""
author: plfiorini
date: 2019-11-17 00:00:00 +0100
image: https://source.unsplash.com/BStW5kYXw4E/400x300
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/BStW5kYXw4E/800x600)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@freestocks?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">freestocks</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

Recent Liri desktop architectural changes made it possible to start the desktop and applications using systemd   For a long time I desired to implement this, but it wasn’t possible before landing some architectural changes.

In this post I will explain how this works and what changes lead to systemd user sessions.


> Before you jump to conclusions, be aware that systemd support is enabled by default but it can be disabled both at build and run time.From a user’s perspective nothing has changed, but this is a fundamental change to push things towards Liri desktop 1.0.

### Advantages

The main advantage of using systemd is that I don’t have to write code to run programs myself and I don’t have to worry about relaunching a vital program if it crashes.

There is already a tool that knows how to manage programs, it works well and have lots of options. So basically instead of writing code myself, I can just pick the right settings and write an INI style file.

There are other advantages as well: systemd allows you to control resources (CPU, memory and I/O) and lets you start programs when they are really needed.

### Architectural changes

In the beginning, session management was part of Liri Shell, but that was just too much stuff for one program.

The first thing to do was to turn liri-sessioninto a C++ program.  
Previously it was just a shell script that was creating the session bus before launching liri-shell.

liri-session:

* sets the environment variables
* create the session bus if needed
* starts up liri-shell and liri-shell-helper, services and applications
* can be controlled via D-Bus
We also needed long running processes to carry out various operations like acting on settings changes, power management, housekeeping, free disk space notifications, …

That’s what liri-daemon is for.

### How does systemd user works

On a systemd managed system, each user is given a user-X.slice([systemd.slice(5)](http://man7.org/linux/man-pages/man5/systemd.slice.5.html)) and the user’s session will be run in a session-Y.scope ([systemd.scope(5)](http://man7.org/linux/man-pages/man5/systemd.scope.5.html)).

There is also user@X.service which is the user’s systemd instance that is shut down when the user logs out.

liri-session starts the liri-session.target unit and uses systemd-run to launch XDG autostart applications in a transient scope.

To ensure that graphical applications are started after the compositor, each XDG autostart application is a systemd unit that depends on liri-shell.target so that their startup is delayed until the graphical environment is up and running.

Some programs (such as pulseaudio) are available as both systemd user units and XDG autostart. We don’t want to start them twice.  
To avoid running them twice, just install a desktop entry of the same name with Hidden=true inside $datadir/liri-session/systemd-user/autostart this will disable the XDG autostart entry.

Liri Shell is made by two components: liri-shell the compositor, and liri-shell-helper a Wayland client that draws parts of the user interface.

With systemd we now have a watchdog that kills liri-shell if it’s stuck for too much time, liri-shell-helper is restarted on crash or if it’s frozen.

Applications in the menu are either started with systemd-run (just like XDG autostart applications) in a transient scope or with D-Bus activation which still means the startup is carried out by systemd due to D-Bus integration with systemd.

  
