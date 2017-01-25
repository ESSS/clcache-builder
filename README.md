# clcache-builder 
## Generates executable and Chocolatey package for clcache.py

This project generates a package with an executable for [clcache.py](https://github.com/frerich/clcache) that is meant to facilitate the usage of `clcache` in a portable way. It is specially useful when needing to use `clcache` in environments with Python 2, since newer versions of `clcache` supports only Python 3.3+.

It also generates a [Chocolatey](https://chocolatey.org/) package that can be downloaded and installed using `choco install`. The advantage of the Chocolatey package is that only `clcache.exe` is added to the PATH (the accompanying `.pyd` and `.dll` files SHOULD NOT be added to the PATH, because they could be accidentally loaded by other programs).

[clcache.py](https://github.com/frerich/clcache) is a little Python script which attempts to avoid unnecessary recompilation by reusing previously cached object files if possible. It is meant to be called instead of the original 'cl.exe' executable. The script analyses the command line to decide whether source code is to be compiled. If so, a cache will be queried for a previously stored object file.

## How to update to a new version

The version in the first line of the `appveyor.yml` file should be changed to the new version.

## How it works

It uses [AppVeyor](https://www.appveyor.com/) to install `pyinstaller` into `Python 3.5` using `pip`, and then using `pyinstaller` to generate `clcache.exe` from the source package downloaded from `clcache` official releases.

The same bundle is then also added to a Chocolatey package using `choco pack`.

## License Terms

The source code of this project is - unless explicitly noted otherwise in the respective files - subject to the [BSD 3-Clause License](https://opensource.org/licenses/BSD-3-Clause).

## Credits

The only relationship of this project with `clcache.py` is that it uses `clcache.py` as a source and generates binary packages for it.
`clcache.py` credits can be found in its page: https://github.com/frerich/clcache#credits
