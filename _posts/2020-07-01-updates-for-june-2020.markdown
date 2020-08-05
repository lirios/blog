---
layout:	post
title: "Updates for June, 2020"
description: "Continuous Integration and OSTree"
author: plfiorini
date: 2020-07-01 19:52:00 +0200
image: https://source.unsplash.com/rjIMBeK3jmE/342x228
tags:
  - updates
---

<figure markdown="1">

![Photo](https://source.unsplash.com/rjIMBeK3jmE/684x456)
<figcaption>
Photo by <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/@glencarrie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Glen Carrie</a>
on <a target="_blank" rel="noopener nofollow" href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</figcaption>

</figure>

## Continuous Integration

CI has been added to [materialdecoration][materialdecoration] and the build issues caused by
qtwayland are fixed nowadays, meaning that the [package][materialdecoration-rpm] now builds again.

## OSTree tools

[ostree-image-creator][oic] and [ostree-upload][ostree-upload] were rewritten with Go, which is
way easier to develop with compared to Rust.

For this kind of applications, Rust didn't give any advantage at all.

[ostree-image-creator][oic] was also redesigned: it's now a tool that builds any kind of image
you want from a declarative recipe.

[image-manager][image-manager] now shares code with [ostree-image-creator][oic] and [ostree-upload][ostree-upload],
for instance all the code to parse JSON and token authentication, and the client was rewritten in Go.

[Here][live-recipe] you can take a look at Liri OS live image recipe.

## OSTree repositories

OSTree [configuration][ostree-config] was revamped and the repository is now GPG signed.
Every night a GitHub workflow builds and uploads the repository.

[materialdecoration]: https://github.com/lirios/materialdecoration
[materialdecoration-rpm]: https://copr.fedorainfracloud.org/coprs/plfiorini/liri-nightly/package/liri-materialdecoration/
[oic]: https://github.com/lirios/ostree-image-creator
[ostree-upload]: https://github.com/lirios/ostree-upload
[image-manager]: https://github.com/liri-infra/image-manager
[live-recipe]: https://github.com/lirios/image-config/blob/develop/live.yaml
[ostree-config]: https://github.com/lirios/ostree-config
