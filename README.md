# Ready-made [Texmacs installers with Hunspell spell checker and more](https://github.com/slowphil/mingw-w64-texmacs/releases) are in the [Releases](https://github.com/slowphil/mingw-w64-texmacs/releases)

## mingw-w64-texmacs : for building the latest TeXmacs in MSys2/Mingw32 environment

when running `makepkg`, this will build TeXmacs for Windows from latest svn and package it with utilities that differ from the official distribution (see the [wiki](https://github.com/slowphil/mingw-w64-texmacs/wiki) for more info): 

- Hunspell spell checker. Hunspell is OpenOffice/LibreOffice's spellchecker, more actively developped than Aspell that ships with the official TeXmacs for windows. Also, for sake of not bloating the package, we pack only the dictionaries for English and the locale of the machine on which the build is made (French for the released installer).

- some command-line tools (used transparently) for better support of SVG images 

- This version of TeXmacs packs several custom plugins:
  - [outline plugin](https://github.com/texmacs/tm-forge/tree/main/miscellanea/outline), to reorganize large documents in a structured manner.
  - [komment plugin](https://github.com/texmacs/tm-forge/tree/main/miscellanea/komments): tools for handling proposed text changes in (offline) collaborative editing
  - [zotexmacs plugin](https://github.com/slowphil/zotexmacs): If you bibliography is handled by [Zotero](https://www.zotero.org/), makes it easy to insert references.
  - [fontawesome plugin](https://github.com/texmacs/tm-forge/tree/main/miscellanea/fontawesome): for using the many web-related icons in Font Awesome free fonts.    
      
    (the equation editor plugin is now a standard feature in the main repo!) 

- A built-in updater tool (will propose an update when I take the time to bring the data here up-to-date... )

The easiest way to build TeXmacs is by using the [fully automated build environment](https://github.com/slowphil/texmacs-win-builder) ([download page](https://github.com/slowphil/texmacs-win-builder/releases/latest))



