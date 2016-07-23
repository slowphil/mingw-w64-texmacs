# PKGBUILD for MinGW-w64 derived from archlinux PKGBUILD - Philippe Joyez   
# archlinux Maintainer: Ronald van Haren <ronald.archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch> # Contributor: Christopher Reimer <c.reimer1993@gmail.com>
# Contributor: wangjiezhe <wangjiezhe AT yandex DOT com>

_realname=texmacs
pkgbase=mingw-w64-${_realname}
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}"
_pkgname=texmacs
pkgver=dernière.
pkgrel=1
pkgdesc="Free scientific text editor, inspired by TeX and GNU Emacs. WYSIWYG editor and CAS-interface. (mingw-w64)"
arch=('any')
url="http://www.texmacs.org/"
license=('GPL')
makedepends=("${MINGW_PACKAGE_PREFIX}-gcc"
             "${MINGW_PACKAGE_PREFIX}-pkg-config"
             )
depends=(
          #"${MINGW_PACKAGE_PREFIX}-aspell"
		  "${MINGW_PACKAGE_PREFIX}-hunspell"
		  "${MINGW_PACKAGE_PREFIX}-wget"
          "${MINGW_PACKAGE_PREFIX}-gc"
          "${MINGW_PACKAGE_PREFIX}-ghostscript"
          "${MINGW_PACKAGE_PREFIX}-imagemagick"
          "${MINGW_PACKAGE_PREFIX}-lcms2"
          "${MINGW_PACKAGE_PREFIX}-freetype"
          "${MINGW_PACKAGE_PREFIX}-iconv"
          "${MINGW_PACKAGE_PREFIX}-qt4"
          "${MINGW_PACKAGE_PREFIX}-guile1.8"
		  "${MINGW_PACKAGE_PREFIX}-poppler-qt4"


        )
source=("${_pkgname}::svn://svn.savannah.gnu.org/texmacs/trunk/src"
        )
sha1sums=('SKIP'
		  )
options=('!emptydirs' '!ccache')
provides=('texmacs')
conflicts=('texmacs')

pkgver() {
  cd "${srcdir}/../${_pkgname}"
  svn info | awk '/Revision/{r=$2}/Date/{gsub(/-/,"");d=$4}END{print d"."r}'
}

prepare() {
  if [ -d "${srcdir}/${_pkgname}-build" ]; then
    rm -rf "${srcdir}/${_pkgname}-build"
  fi 
  mv "${srcdir}/${_pkgname}" "${srcdir}/${_pkgname}-build"
  # svn export "${srcdir}/${_pkgname}" "${srcdir}/${_pkgname}-build"

  cd "${srcdir}/${_pkgname}-build"

  patch -i ../../qt_m4.patch -p2
  patch -i ../../raux_win.patch -p0
  autoreconf
  
  patch -i ../../configure.patch -p2

  sed -i 's|#! /bin/sh|#! /bin/bash|' configure
}

build() {
  export GUILE_LOAD_PATH="${MINGW_PREFIX}/share/guile/1.8"

  cd "${srcdir}/${_pkgname}-build"

./configure \
    --prefix=${MINGW_PREFIX} \
    --build=${MINGW_CHOST} \
    --host=${MINGW_CHOST} \
    --with-guile="/mingw32/bin/guile-config" \
	--with-qt="/mingw32/bin/" \
	--enable-console #--enable-debug

  make -j$(nproc)
}

package() {
export TM_BUILD_DIR="${srcdir}/${_pkgname}-build"
export BUNDLE_DIR="${srcdir}/TeXmacs-Windows"

###############################################################################
# Make a Windows installer
# here we mimick what would do "make WINDOWS_BUNDLE", plus our own extras
###############################################################################


GS_DLL=( gswin32c.exe libiconv-2.dll  zlib1.dll  libtiff-5.dll  libpng16-16.dll \
  liblcms2-2.dll  libbz2-1.dll  libopenjp2-7.dll  libintl-8.dll  libidn-11.dll \
 liblzma-5.dll  libpcre-1.dll  libjpeg-8.dll  libgs-9.dll  libglib-2.0-0.dll \
 libwinpthread-1.dll  libharfbuzz-0.dll  libgraphite2.dll  libfreetype-6.dll \
 libgcc_s_dw2-1.dll  libstdc++-6.dll )

HUNSPELL_DLL=( hunspell.exe libiconv-2.dll libintl-8.dll libwinpthread-1.dll \
  libhunspell-1.4-0.dll libgcc_s_dw2-1.dll libstdc++-6.dll )

PDFTOCAIRO_DLL=( pdftocairo.exe libiconv-2.dll zlib1.dll libtiff-5.dll \
 libpng16-16.dll liblcms2-2.dll libbz2-1.dll libexpat-1.dll libpixman-1-0.dll \
 libopenjpeg-5.dll libintl-8.dll liblzma-5.dll libpcre-1.dll libjpeg-8.dll \
 libcairo-2.dll libglib-2.0-0.dll libwinpthread-1.dll libharfbuzz-0.dll \
 libgraphite2.dll libfreetype-6.dll libfontconfig-1.dll libgcc_s_dw2-1.dll \
 libstdc++-6.dll libpoppler-62.dll )

TEXMACS_DLL=( libbz2-1.dll libharfbuzz-0.dll libjpeg-8.dll liblcms2-2.dll \
  libopenjpeg-5.dll libsystre-0.dll libtiff-5.dll libwinpthread-1.dll \
  libgcc_s_dw2-1.dll QtCore4.dll QtGui4.dll QtXml4.dll libgmp-10.dll \
  libguile-17.dll libfreetype-6.dll libltdl-7.dll libiconv-2.dll libintl-8.dll \
  libstdc++-6.dll libpoppler-62.dll libpoppler-qt4-4.dll libpng16-16.dll zlib1.dll \
  libglib-2.0-0.dll libgraphite2.dll liblzma-5.dll libtre-5.dll libpcre-1.dll )
  
#WINSPARKLE_DLL = 
#WINSPARKLE_PATH = 

QT_NEEDED_PLUGINS_LIST=( accessible imageformats )

GS_UTILS_PATH=/mingw32/share/ghostscript/9.19/lib/
GS_UTILS=( ps2epsi.ps ps2epsi.bat cat.ps gssetgs.bat )

rm -r -f $BUNDLE_DIR

if test ! -d $BUNDLE_DIR ; then
  mkdir -p $BUNDLE_DIR
fi

cd $TM_BUILD_DIR
if test -f $BUNDLE_DIR/bin/texmacs.exe ; then
  rm $BUNDLE_DIR/bin/texmacs.*
fi

cp -r -f  -u TeXmacs/* $BUNDLE_DIR/

mv -f $BUNDLE_DIR/bin/texmacs.bin $BUNDLE_DIR/bin/texmacs.exe
rm -f -r $BUNDLE_DIR/bin/texmacs
cp -r -f misc/admin/texmacs_updates_dsa_pub.pem $BUNDLE_DIR/bin
cp -r -f packages/windows/*.exe $BUNDLE_DIR/bin

cd /mingw32/bin

for DLL in "${TEXMACS_DLL[@]}" ; do
cp -u $DLL $BUNDLE_DIR/bin
done
for DLL in "${PDFTOCAIRO_DLL[@]}" ; do
cp -u $DLL $BUNDLE_DIR/bin
done
for DLL in "${GS_DLL[@]}" ; do
cp -u $DLL $BUNDLE_DIR/bin
done
for DLL in "${HUNSPELL_DLL[@]}" ; do
cp -u $DLL $BUNDLE_DIR/bin
done
cp -u wget.exe $BUNDLE_DIR/bin

for PLUGIN in "${QT_NEEDED_PLUGINS_LIST[@]}"; do
            cp -r -f -u /mingw32/share/qt4/plugins/$PLUGIN $BUNDLE_DIR/bin
        done

mkdir $BUNDLE_DIR/dict
export GUILE_LOAD_PATH="${MINGW_PREFIX}/share/guile/1.8"
find `guile-config info pkgdatadir` -type d -name ice-9 -exec cp -r -f {} $BUNDLE_DIR/progs/ \;

### this (taken from git for windows sdk) works, just need to filter out Windows dlls
#dlls_for_exes () {
#	# Add DLLs' transitive dependencies
#	dlls=
#	todo="$* "
#	while test -n "$todo"
#	do
#		path=${todo%% *}
#		todo=${todo#* }
#		case "$path" in ''|' ') continue;; esac
#		for dll in $(objdump -p "$path" |
#			sed -n 's/^\tDLL Name: /mingw32\/bin\//p')
#		do
#			case "$dlls" in
#			*"$dll"*) ;; # already found
#			*) dlls="$dlls $dll"; todo="$todo /$dll ";;
#			esac
#		done
#	done
#	echo "$dlls"
#}

#echo $(dlls_for_exes $(ls "$BUNDLE_DIR/bin/texmacs.exe"))


#TARGET="$HOME"/texmacs-installer.7z.exe
OPTS7="-m0=lzma -mx=9 -md=64M"
TMPPACK="${srcdir}/tmp.7z"
TARGET="/texmacs_installer.7z.exe"

fileList=$BUNDLE_DIR


echo "Creating archive" &&
(cd / && 7za a $OPTS7 "$TMPPACK" $fileList) &&
(cat "/7zSD.sfx" &&
 echo ';!@Install@!UTF-8!' &&
 echo 'Title="TeXmacs for Windows"' &&
 echo 'BeginPrompt="This archive extracts TeXmacs for Windows"' &&
 echo 'CancelPrompt="Do you want to cancel TeXmacs installation?"' &&
 echo 'ExtractDialogText="Please, wait..."' &&
 echo 'ExtractPathText="Where do you want to install TeXmacs?"' &&
 echo 'ExtractTitle="Extracting..."' &&
 echo 'GUIFlags="8+32+64+256+4096"' &&
 echo 'GUIMode="1"' &&
 #echo 'InstallPath="C:\\git-sdk-'$BITNESS'"' &&
 echo 'InstallPath="C:\\Program Files (x86)\\TeXmacs"' &&
 echo 'OverwriteMode="2"' &&
 #echo 'ExecuteFile="%%T\setup-git-sdk.bat"' &&
 #echo 'Delete="%%T\setup-git-sdk.bat"' &&
 echo ';!@InstallEnd@!' &&
 cat "$TMPPACK") > "$TARGET" &&
echo "Success! You will find the new installer at \"$TARGET\"." &&
echo "It is a self-extracting .7z archive." &&
rm $TMPPACK


}

