# Ready-made [Texmacs installers with spell checker and more](https://github.com/slowphil/mingw-w64-texmacs/releases) are in the [Releases](https://github.com/slowphil/mingw-w64-texmacs/releases)

## mingw-w64-texmacs : for building the latest TeXmacs in MSys2/Mingw32 environment

when running `makepkg`, this will build TeXmacs for Windows from latest svn and package it with utilities that differ from the official distribution (see the [wiki](https://github.com/slowphil/mingw-w64-texmacs/wiki) for more info): 

- Hunspell spell checker (with dictionary for English and the locale of the machine on which the build is made -- French for the released installer).

- Extra image utilities enabling to use TeXmacs as an equation editor for Inkscape and LibreOffice (using this [LO extension](https://github.com/slowphil/SVG_and_TeXmacs_for_LibreOffice)).

- A built-in updater tool.

The easiest way to build TeXmacs is by using the [fully automated build environment](https://github.com/slowphil/texmacs-win-builder) ([download page](https://github.com/slowphil/texmacs-win-builder/releases/latest))



