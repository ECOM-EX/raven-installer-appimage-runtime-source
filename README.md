# AppImage runtime source used by Raven Installer

Every AppImage made with **Raven Installer** (by ECOM Extensions Pty Ltd) starts with the
AppImage type 2 runtime, unmodified, built from this exact source:

- **AppImage type 2 runtime**, commit [`fedfad5`](https://github.com/AppImage/type2-runtime/commit/fedfad51acc2860b2916a1eef32ba4a500ff31ef) (MIT, see `LICENSE`).
  This repository is that commit with its full history, plus the folder `third-party-source/`.
  The upstream README is in `README-upstream.md`.
- **libfuse 3.15.0** (GNU Lesser General Public License 2.1), statically linked into the runtime.
  Source: `third-party-source/fuse-3.15.0.tar.xz`. The runtime build applies
  `patches/libfuse/mount.c.diff` to it.
- **squashfuse 0.5.2** (BSD-2-Clause): `third-party-source/squashfuse-0.5.2.tar.gz`.
- musl libc, zlib and zstd come from Alpine Linux packages during the build (see
  `scripts/docker/Dockerfile` and `scripts/chroot/`).

Checksums are in `third-party-source/SHA256SUMS`. They match the ones checked by
`scripts/common/install-dependencies.sh`.

## Rebuilding the runtime, for example with a changed libfuse

Follow `README-upstream.md` (`scripts/docker/build-with-docker.sh` or `scripts/chroot/build.sh`).
To use your own libfuse, change `scripts/common/install-dependencies.sh` to unpack your copy
instead of downloading `fuse-3.15.0.tar.xz`. The result can replace the first part of any
AppImage made with Raven Installer: the runtime is a separate program placed in front of the
app's file system and is not linked with the app.

## Which Raven Installer versions use this

Raven Installer 0.1.x. This repository is kept online for as long as Raven Installer ships this
runtime, and for at least three years after the last release that does.
