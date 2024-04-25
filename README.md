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
podman build --security-opt=label=disable --cap-add=all --device /dev/fuse \
  -t localhost/fedora-bootc:40 -f Containerfile.fedora-40
```

See `Containerfile.fedora-40` for more details.

You are of course also free to fork, customize, and build base images yourself.
See this page[6] of the documentation for more information.

## More information

Documentation: <https://docs-bootc-org-fedora-bootc-6570d042ee03afe91a435802a9746be5039.gitlab.io/fedora-bootc/>

## Badges

| Badge                   | Description          | Service      |
| ----------------------- | -------------------- | ------------ |
| [![Renovate][1]][2]     | Dependencies         | Renovate     |
| [![Pre-commit][3]][4]   | Static quality gates | pre-commit   |

[1]: https://img.shields.io/badge/renovate-enabled-brightgreen?logo=renovate
[2]: https://renovatebot.com
[3]: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit
[4]: https://pre-commit.com/
[5]: https://docs-bootc-org-fedora-bootc-6570d042ee03afe91a435802a9746be5039.gitlab.io/fedora-bootc/building-containers/
[6]: https://docs-bootc-org-fedora-bootc-6570d042ee03afe91a435802a9746be5039.gitlab.io/fedora-bootc/building-custom-base/
