# clcache-builder 
## NOTE

This project is now deprecated as it is merged in the [official `clcache` repo](https://github.com/frerich/clcache). Will be kept here for reference for a short time.

See: https://github.com/frerich/clcache/pull/267

## Generates executable and Chocolatey package for clcache.py

[![Latest version released](https://img.shields.io/chocolatey/v/clcache.svg)](https://chocolatey.org/packages/clcache)
[![Package downloads count](https://img.shields.io/chocolatey/dt/clcache.svg)](https://chocolatey.org/packages/clcache)
[![Build status](https://ci.appveyor.com/api/projects/status/ci8xpk1wa0e8qyxh/branch/master?svg=true)](https://ci.appveyor.com/project/ESSS/clcache-builder/branch/master)

This project generates a package with an executable for [clcache.py](https://github.com/frerich/clcache) that is meant to facilitate the usage of `clcache` in a portable way. It is specially useful when needing to use `clcache` in environments with Python 2, since newer versions of `clcache` supports only Python 3.3+.

It also generates a [Chocolatey](https://chocolatey.org/) package that can be downloaded and installed using `choco install`. The advantage of the Chocolatey package is that only `clcache.exe` is added to the PATH (the accompanying `.pyd` and `.dll` files SHOULD NOT be added to the PATH, because they could be accidentally loaded by other programs).

[clcache.py](https://github.com/frerich/clcache) is a little Python script which attempts to avoid unnecessary recompilation by reusing previously cached object files if possible. It is meant to be called instead of the original 'cl.exe' executable. The script analyses the command line to decide whether source code is to be compiled. If so, a cache will be queried for a previously stored object file.

## How to install

After the package is published on [Chocolatey](https://chocolatey.org/packages/clcache) it may be installed using:

`choco install clcache`

Or, for a specific version:

`choco install clcache -version 4.0.0`

## How to update to a new version

In the `appveyor.yml` file, change the version in the first line and in the `CLCACHE_VERSION` environment variable to reflect the new version.

Create a new release on GitHub with a tag such as `v4.0.0` and a name such as `clcache 4.0.0`. A new build will be triggered, and the artifacts published by AppVeyor.

Artifacts are published by AppVeyor from builds in tagged commits in the `master` branch. These artifacts should be attached to the GitHub release, and the `.nupkg` package uploaded to Chocolatey.

## How it works

It uses [AppVeyor](https://www.appveyor.com/) to install `pyinstaller` into `Python 3.4` using `pip`, and then using `pyinstaller` to generate `clcache.exe` from the source package downloaded from `clcache` official releases.

The same bundle is then also added to a Chocolatey package using `choco pack`.

Note that `Python 3.4` is currently used because there is an issue when running the `Python 3.5` PyInstaller executable on older operating systems such as Windows Vista.

## License Terms

The source code of this project is - unless explicitly noted otherwise in the respective files - subject to the [BSD 3-Clause License](https://opensource.org/licenses/BSD-3-Clause).

## Credits

The only relationship of this project with `clcache.py` is that it uses `clcache.py` as a source and generates binary packages for it.
`clcache.py` credits can be found in its page: https://github.com/frerich/clcache#credits
