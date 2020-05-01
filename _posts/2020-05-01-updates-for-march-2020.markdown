---
layout:	post
title: "Updates for March, 2020"
description: "XDG portal improvements and OS installer fixes"
author: plfiorini
date: 2020-05-01 08:00:00 +0200
image: https://source.unsplash.com/5eyAJMTb6mM/400x266
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/5eyAJMTb6mM/800x533)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@glencarrie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Glen Carrie</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

Flatpak is a first class citizen in Liri OS.

For this reason during March our XDG portal implementation was improved.

UI creation now works way better and QML code is integrated with C++, however at the moment
there is no XDG foreign support.  This means that portal dialogs are not parented to the
application window.

The following portals were created:

 * Screenshot
 * Lockdown
 * Print
 * Access
 * Settings
 * Background
 * Wallpaper

The screenshot portal has a method to pick the color of a pixel, so in order to
make this possible I created a custom Wayland protocol.

While working on the screenshot portal, I also improved our implementation of
the screen copy Wayland [protocol][protoxml] from wlroots.

Image format conversion was fixed, it's now possible to capture with or without the
pointer cursor as well as memory leak fixes.

In other news, the OS installer was fixed so it's now possible to install it again.
However the boot loader configuration needs some fixes that will be probably implemented
in May.

[protoxml]: https://github.com/lirios/wayland/blob/develop/data/protocols/wlr-screencopy-unstable-v1.xml
