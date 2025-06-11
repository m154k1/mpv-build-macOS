# mpv-build-macOS

[![Build & Upload Artifact](https://github.com/m154k1/mpv-build-macOS/actions/workflows/build.yml/badge.svg)](https://github.com/m154k1/mpv-build-macOS/actions/workflows/build.yml)
[![Lint](https://github.com/m154k1/mpv-build-macOS/actions/workflows/lint.yml/badge.svg)](https://github.com/m154k1/mpv-build-macOS/actions/workflows/lint.yml)

A set of scripts that help build [mpv](https://mpv.io) on macOS.

> [!TIP]
> Prebuilt mpv.app from GitHub Actions is available at [nightly.link].
>
> Download: [`mpv-macos-15-arm64.zip`] (macOS 15.5 & Apple M1 or newer)

### Requirements

- [Xcode.app](https://developer.apple.com/xcode/)
- [Homebrew](https://brew.sh)

### Build and install

:arrow_right: Make sure Xcode is ready:

```sh
xcodebuild -runFirstLaunch
```

:arrow_right: Clone the repository:

```sh
git clone "https://github.com/m154k1/mpv-build-macOS.git"
cd mpv-build-macOS
```

:arrow_right: Install build dependencies from Homebrew:

```sh
xargs brew install --formula < homebrew/build-deps.txt
```

:arrow_right: Create an installation directory for local packages:

> [!NOTE]
> If you want to use custom installation directory,
> set `PREFIX` environment variable instead.

```sh
sudo mkdir /opt/local
sudo chown "$USER":admin /opt/local
mkdir /opt/local/stow
```

:arrow_right: Fetch sources:

```sh
./fetch all
```

:arrow_right: Build mpv and its dependencies (select an option):

- Install mpv as CLI-only program:

  ```sh
  ./build-all
  ```

- Install CLI and create an app bundle (mpv.app):

  ```sh
  ./build-all --bundle
  ```

  The bundle will be placed in `mpv.tar.gz`.

:arrow_right: Add `/opt/local/bin` (or `$PREFIX/bin`) to your `$PATH`.

### Recommended settings

```cfg
# ~/.config/mpv/mpv.conf
vo=gpu-next
hwdec=videotoolbox
macos-render-timer=feedback
```

### Environment variables

- `MVK_CONFIG_LOG_LEVEL=<value>` - sets MoltenVK log level:

  - `0` - disabled
  - `1` - error
  - `2` - warning
  - `3` - verbose

- `MTL_HUD_ENABLED=1` - enables the [Metal Performance HUD].

[nightly.link]: https://nightly.link/m154k1/mpv-build-macOS/workflows/build/master
[`mpv-macos-15-arm64.zip`]: https://nightly.link/m154k1/mpv-build-macOS/workflows/build/master/mpv-macos-15-arm64.zip
[Metal Performance HUD]: https://developer.apple.com/documentation/xcode/monitoring-your-metal-apps-graphics-performance
