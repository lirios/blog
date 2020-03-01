---
layout:	post
title: "Updates for January, 2020"
description: "Focus on Liri OS live images"
author: plfiorini
date: 2020-02-28 13:05:11 +0100
image: https://source.unsplash.com/TGeFx4x4NHU/400x300
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/TGeFx4x4NHU/800x600)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@glencarrie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Glen Carrie</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

January was all about making progress on how Liri OS live images.

Previously, the images were made with traditional packages with [kickstart](https://github.com/lirios/kickstart) files.

I wrote a Python module for the [Calamares](https://calamares.io) installer, that deploys the OS tree into the root partition.
However this is excruciatingly slow because at the moment we don't have a fast Web site, in order to reduce costs
(all the expenses are out of my wallet).

If the image is made with OSTree itself, the same repository on the image can be used to deploy the operating system
on the root partition, without involving the network at all.

At the time of my research for already existing tools, nothing was found.
Then Fedora CoreOS started doing something [like that](https://github.com/coreos/coreos-assembler), but it's too
complex and focused on their needs.

So I came up with [oic](https://github.com/lirios/ostree-image-creator), also known as ostree-image-creator.

It's a simple tool written with Rust, that creates live images.
You can use it with [ostree](https://github.com/ostreedev/ostree), it doesn't need [rpm-ostree](https://github.com/coreos/rpm-ostree).

In the future it will be extended to disk images as well.

Our OSTree repository now has a live branch, derived from the actual branch that will be installed on users' computers.
The live branch installs [Calamares](https://calamares.io) and `dracut` modules specific to its bootstrap, plus
a setup service that creates the `liveuser` user.

The difference with the previous images is that only `/etc` and `/var` are writable, and they are not persistent.

Another important Rust program was made: [ostree-upload](https://github.com/lirios/ostree-upload).

We build the OSTree repository in a separate CI machine and want to upload the objects to the public
OSTree repository.

This program receives the objects from the CI machine and store them in a temporary directory, until the process is done.
Once all objects are transfered, the new changes are published.

This is better than using `rsync`, there's no risk that users will fetch from the OSTree repository
during a synchronization.
