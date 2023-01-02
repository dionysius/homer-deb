# deb packaging for homer

This debian source package builds [homer](https://github.com/bastienwirtz/homer) natively on your build environment. This debian source is managed with [git-buildpackage](https://wiki.debian.org/PackagingWithGit) and is aimed to provide a pretty good quality debian source package (where possible so far). You can find the maintaining command summary in [debian/gbp.conf](debian/gbp.conf).

## Download prebuilt packages

Prebuilt deb packages are available in the [releases section](https://github.com/dionysius/homer-deb/releases) for latest Ubuntu LTS. I'd liked to include also debian stable, but [there are no debian images available in github actions](https://github.com/actions/runner-images).

They are built in [Github Actions](https://github.com/dionysius/homer-deb/actions) and automatically created on a debian tag push and released on a successful build.

## Requirements

- Installed `git-buildpackage` `debhelper-compat`
- All build dependencies as defined in [debian/control](debian/control) are installed (it will notify you in the build process as well)
  - [`mk-build-deps`](https://manpages.debian.org/testing/devscripts/mk-build-deps.1.en.html) can help you automate the installation
- If `yarnpkg`/`nodejs` is not recent enough
  - Don't forget to look into your `*-updates` apt sources for newer versions
  - This debian source also supports those installed with help of [`nvm`](https://github.com/nvm-sh/nvm)
    - Requires preloaded `nvm use <version>` before invoking packaging
    - Yarn needs to be installed with alias and "pseudo-globally" (thanks to nvm) using: `npm install -g yarnpkg@npm:yarn`

## Packaging

- Clone with help of git-buildpackage: `gbp clone https://github.com/dionysius/homer-deb.git`
- Switch to the folder: `cd homer-deb`
- Build with help of git-buildpacke: `gbp buildpackage`
  - There are many arguments to fine tune how it is built (see `gbp buildpackage --help` and `dpkg-buildpackage --help`)
  - Mine are usually: `-b` (binary-only, no source files), `-us` (unsigned source package), `-uc` (unsigned .buildinfo and .changes file), `--git-export-dir=<somedir>` (before building the package export the source there)

## TODOs

- Phase 1: Automatic notification on new upstream version. Phase 2: Automatic PR with updates from upstream
- Sign the packages
