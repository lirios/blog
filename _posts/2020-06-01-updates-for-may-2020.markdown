---
layout:	post
title: "Updates for May, 2020"
description: "Continuous Integration"
author: plfiorini
date: 2020-06-01 09:52:00 +0200
image: https://source.unsplash.com/xEG5Agjb_5s/228x342
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/xEG5Agjb_5s/456x684)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@glencarrie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Glen Carrie</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

During may the continuous integration improvements continued.

## Translations

There is now a new [translation action][translation-action] that regenerates translation sources
and push them to Transifex, pull the rebased and updated translations, merge translations into
desktop and metainfo files, then commit and push to git.

All in one action.

We now have metainfo translated, desktop files are translated with gettext and there is
context information that indicates which key is being translated.

## Build

The build workflow got some improvements.  Previously we were building on Ubuntu with the
[ppa-beineri][ppa-beineri] repository so we can build against multiple Qt versions.

However [ppa-beineri][ppa-beineri] doesn't build with EGL support, but this makes building
[eglfs][eglfs] impossible.

In order to overcome this difficulty, there are OpenSuSE Tumbleweed images now
with all the dependencies.  One image for each Qt version we are building against.

At the time of this writing, the Qt versions supported are 5.12 because it's a LTS release,
then the latest two version 5.14 and 5.15.

All container images are in the same [repository][container-images].

## Documentation

The developer documentation, previously available through [readthedocs.org][readthedocs]
is now available via GitHub Pages on [docs.liri.io][docs].

[translation-action]: https://github.com/liri-infra/translation-action
[ppa-beineri]: https://launchpad.net/~beineri
[eglfs]: https://github.com/lirios/eglfs
[container-images]: https://github.com/liri-infra/container-images
[readthedocs]: https://readthedocs.org
[docs]: https://docs.liri.io
