---
layout:	post
title: "Updates for April, 2020"
description: "Continuous Integration"
author: plfiorini
date: 2020-05-01 09:52:00 +0200
image: https://source.unsplash.com/P6YxhqqcFJ4/400x266
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/P6YxhqqcFJ4/800x533)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@glencarrie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Glen Carrie</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

April didn't see much code improvements, it was pretty much dedicated
to the continuous integration.

Previously we used [Travis CI][travis] and [AppVeyor][appveyor] as continuous integration
for pushes and pull requests, and [Jenkins][jenkins] to build the OSTree repository, OS images
and translation updates.

Now with [GitHub Actions][actions] we can really improve the Liri CI.

GitHub Actions introduce the concept of workflows, this gives us great flexibility to implement whatever we want.

We now have basically three workflows:

 * Status check and validation
 * Build and release
 * Translations

We can see if each commit or pull request has valid QML and freedesktop.org files (desktop entries and
AppStream metadata) with the following actions that I developed for Liri and will be in the marketplace soon:

 * [qmllint-action](https://github.com/liri-infra/qmllint-action)
 * [xdg-validator-action](https://github.com/liri-infra/xdg-validator-action)

And also prevent work in progress pull requests to be merged.

In the future we can also check for the proper SPDX license information or whether there are coding style violations.

With the build workflow we can check if the code builds on different operating systems, platforms and compilers.
The cross-platform apps benefit by this the most as we can build against different Qt versions, Linux, Windows, macOS and Flatpak.
In the future we'll probably add Snap and AppImage.
The resulting artifacts are available for each run of the workflow.
When a new version is released, the artifacts are attached to the release automatically.

When a library is built in the CI, the workflow stores a `.tar.gz` artifact with the binaries
that will be used by the CI of another repository that depends on that library.
Given that you cannot download artifacts from another repository with the official
[actions/download-artifact](https://github.com/actions/download-artifact),
I made my [fetch-artifact](https://github.com/liri-infra/fetch-artifact) action.

Every week the translation sources are regenerated and sent to [Transifex][transifex].
The translations, now rebased to the new sources, are downloaded and automatically committed.
This was previously done in our private Jenkins installation, but the workflows are easier
to configure and manage.  This also result in less work on our private build server.

These are the actions I made for the translations:

 * [lupdate-action](https://github.com/liri-infra/lupdate-action)
 * [transifex-action](https://github.com/liri-infra/transifex-action)

Then I made the [.github repository](https://github.com/lirios/.github) that contains default
GitHub files, the so called [community health files][community-health] such as code of conduct,
contributing guidelines, issue template and pull request template.
This is yet another step towards a better GitHub integration.

[travis]: https://travis-ci.org/
[appveyor]: https://www.appveyor.com/
[jenkins]: https://www.jenkins.io/
[actions]: https://github.com/features/actions
[transifex]: https://www.transifex.com/lirios/
[community-health]: https://help.github.com/en/github/building-a-strong-community/creating-a-default-community-health-file
