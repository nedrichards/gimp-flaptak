# gimp-flaptak
Flatpak recipe for the Gimp. This is an adapatation of the upstream manifest to work with the latest developer release rather than just git.

Installing:
-----------
If you just want to run the app then install the [prebuilt flatpak bundle](https://github.com/nedrichards/gimp-flatpak/raw/master/org.gimp.GIMP.flatpak). Just download it and double click to install.


Instructions:
-------------

(1) Install the flatpak repository for GNOME:
```
flatpak remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo

```
(2) Install the required runtimes
```
  flatpak install gnome org.gnome.Sdk
  flatpak install gnome org.gnome.Platform
```
(3) Build the app from this directory:
```
flatpak-builder --force-clean --ccache --require-changes --repo=repo app org.gimp.GIMP.json
```
(4) Add a remote to your local repo and install it:
```
flatpak --user remote-add --no-gpg-verify gimp-repo /path/to/your/flatpak/repo
flatpak --user install gimp-repo org.gimp.GIMP
```
(5) Run the GIMP:
```
flatpak run org.gimp.GIMP
```

Gives you the list. You can access files within your home folder by default.

Note that if you do further changes in the `appdir` (e.g. to the metadata) you'll need to update before running it again:
```
flatpak --user update org.gimp.GIMP
```

Last, you can bundle it to a file with the `build-bundle` subcommand:
```
flatpak build-bundle /path/to/your/flatpak/repo org.gimp.GIMP.flatpak org.gimp.GIMP
```
