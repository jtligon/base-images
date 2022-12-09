# Demonstration base images for use with bootc

This repository contains "base images" suitable for use with [bootc](https://github.com/containers/bootc).

These images are technology demonstrators, not for production use.  The intention is that these images are
generated by the OS vendor or distribution.  Or, you can fork this repository and generate your own
via `rpm-ostree compose image`.


# Building

Here's an example command:

```
$ sudo rpm-ostree compose image --authfile ~/.config/containers/myquay.json --cachedir=cache -i --format=registry fedora.yaml quay.io/cgwalters/fedora-oscore
```

More information at https://coreos.github.io/rpm-ostree/container/