## Build Titlebar Branch

To build the titlebar branch, run the following commands:

```bash
$ git clone -b titlebar --depth 1 --signle-branch https://github.com/anassahmed/firefox-flatpak
$ cd firefox-flatpak
$ ./setup_runtime.sh
$ ./build.sh org.mozilla.FirefoxNightlyTitlebar # for the normal nightly
$ ./build.sh org.mozilla.FirefoxNightlyWaylandTitlebar # wayland
$ flatpak remote-add --user --no-gpg-verify nightly-firefox-local ./repo
$ flatpak --user -v install nightly-firefox-local org.mozilla.FirefoxNightlyTitlebar # normal one
$ flatpak --user -v install nightly-firefox-local org.mozilla.FirefoxNightlyWaylandTitlebar # wayland one
$ flatpak run org.mozilla.FirefoxNightlyTitlebar # normal one
$ flatpak run org.mozilla.FirefoxNightlyWaylandTitlebar # wayland one
```

It should take only an hour to compile on a quad-core CPU (8 threads), not
counting the time it needs to download sources (based on your internet
connection speed).

### Wayland Version

The `titlebar-csd` branch doesn't have the `wayland` commits, so obviously it
doesn't work (if you can fork `stransky/gecko-dev` and merge the `titlebar`
branch with `master` branch as the latter has the wayland commits, you're
welcome).

## Normal Nightly Version

It's confused with the main firefox app (if you've an already opened firefox
app, it will open a new window, so you should close all firefox instances
before using it.)

## Bundled Flatpaks

The `./build.sh` scripts produces `*.flatpak` packages at the end, but they're
not usable (at least for me) unless you provide `$GPG_BUNDLE_SETTINGS` as an
environment variable for the script
(I assume they're `--gpg-homedir <gpg-dir-path> --gpg-keys <key>
--gpg-sign=<key-fignerprint>`),
you can read more about it in `man flatpak-build-bundle`.

The binary bundles are available here:

1. [Normal Nightly with Titlebar branch patches](https://www.dropbox.com/s/uso9f501d8bgxkx/org.mozilla.FirefoxNightlyTitlebar.flatpak?dl=0)

2. [Wayland Nightly with Titlebar branch patches](https://www.dropbox.com/s/80tdqbt0vd62qpg/org.mozilla.FirefoxNightlyWaylandTitlebar.flatpak?dl=0)
