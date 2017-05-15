thunderbird-flatpak
===================

Resources to build Mozilla Thunderbird as a flatpak.

Requirements:
------------

  * flatpak >= 0.8.2
  * flatpak-builder >= 0.8.2
  * org.gnome Platform and Sdk runtimes

Instructions:
-------------

(1) Install the flatpak repository for GNOME:
```
  flatpak remote-add --if-not-exists gnome https://sdk.gnome.org/gnome.flatpakrepo
```
(2) Install the required runtimes
```
  flatpak install gnome org.gnome.Platform
  flatpak install gnome org.gnome.Sdk
```
(3) Build thunderbird from this directory:
```
  flatpak-builder --force-clean --ccache --require-changes \
      --repo=repo app \
      org.mozilla.Thunderbird.json
```
(4) Add a remote to your local repo and install it:
```
  flatpak --user remote-add --no-gpg-verify thunderbird-repo /path/to/your/flatpak/repo
  flatpak --user install thunderbird-repo org.mozilla.Thunderbird
```
(5) Run thunderbird as an flatpak:
```
  flatpak run org.mozilla.Thunderbird
```

Note that if you do further changes in the `appdir` (e.g. to the metadata), you'll need to re-publish it in your local repo and update before running it again:
```
  flatpak build-export /path/to/your/flatpak/repo /path/to/flatpak/appdir
  flatpak --user update org.mozilla.Thunderbird
```

Lastly, you can bundle Thunderbird to a file with the `build-bundle` subcommand:
```
  flatpak build-bundle /path/to/your/flatpak/repo org.mozilla.Thunderbird.flatpak org.mozilla.Thunderbird
```