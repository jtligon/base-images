# Fedora bootc base images

Create and maintain base *bootable* container images from Fedora packages.

## Motivation

The original Docker container model of using "layers" to model applications has
been extremely successful. This project aims to apply the same technique for
bootable host systems - using standard OCI/Docker containers as a transport and
delivery format for base operating system updates.

## Building

First, the expectation is that most users will want to build *layered* images
on top of the official base images. See the documentation[5] for more info.

Building the images in this repo can be done with `podman build` as with any
other application image (note that building with `docker` is not currently
supported). You need to enable some privileges for technical reasons.

```
podman build --security-opt=label=disable --cap-add=all \
  --device /dev/fuse -t localhost/fedora-bootc .
```

See the `Containerfile` for more details.

You are of course also free to fork, customize, and build base images yourself.
See this page[6] of the documentation for more information.

## Tiers

There are currently 3 tiers:
- **tier-0**: This image is more of a convenient centralization point for CI
  and curation around a package set that we can all agree is the rough minimum
  necessary for a usable system. It's not meant to be used as is, but layered
  upon.
- **tier-1**: This image is much larger and notably includes networking and
  firmwares. It's a good starting point onto which you can do less
  customizations to get what you need.
- **tier-x**: This image is not intended for end-users. It's the shared base
  used by all image-based Fedora variants (IoT, Atomic Desktops, and CoreOS).
  Changes to this tier may be done without accounting for external users.

**tier-1** inherits from **tier-x** and **tier-x** in turn inherit from **tier-0**.

All non-trivial changes to **tier-0** and **tier-x** should be ACKed by at least
one stakeholder of each Fedora variant WGs.

## More information

Documentation: <https://docs.fedoraproject.org/en-US/bootc/>

## Badges

| Badge                   | Description          | Service      |
| ----------------------- | -------------------- | ------------ |
| [![Renovate][1]][2]     | Dependencies         | Renovate     |
| [![Pre-commit][3]][4]   | Static quality gates | pre-commit   |

[1]: https://img.shields.io/badge/renovate-enabled-brightgreen?logo=renovate
[2]: https://renovatebot.com
[3]: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit
[4]: https://pre-commit.com/
[5]: https://docs.fedoraproject.org/en-US/bootc/building-containers/
[6]: https://docs.fedoraproject.org/en-US/bootc/building-custom-base/
