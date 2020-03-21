---
layout:	post
title: "Updates for February, 2020"
description: "New blog and screencast improvements"
author: plfiorini
date: 2020-03-21 21:00:00 +0100
image: https://source.unsplash.com/N8MDgWvUW-8/400x266
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/N8MDgWvUW-8/800x533)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@glencarrie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Glen Carrie</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

February was mostly about working on this blog.

You can read more about it [here][blogpost].

This month we also ported the [screencast program][screencast] to GStreamer, in place of
GStreamerQt that has been abandoned.

The app now uses the portal API to start the screencast session, this means
that it will work with any other desktop environment with a portal implementation.

Meanwhile, our portal implementation has been improved and can now make screencasts
without CPU effort using DMA-BUFs.

[eglfs][eglfs] had to be changed to support passing file
descriptors to the compositor, that now implements the [wlr-export-dmabuf-unstable-v1][protoxml]
protocol from wlroots.


[blogpost]: /welcome-to-the-new-blog
[screencast]: https://github.com/lirios/screencast
[eglfs]: https://github.com/lirios/eglfs
[protoxml]: https://github.com/lirios/wayland/blob/develop/data/protocols/wlr-export-dmabuf-unstable-v1.xml
