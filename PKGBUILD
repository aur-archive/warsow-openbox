# $Id$
# Submiter: Ivo Nunes <netherblood@gmail.com>
# Mantainer: Vasco nunes <vascomfnunes@gmail.com>
# Patch created by K1ll from the Warsow forums

pkgname=warsow-openbox
pkgver=1.03
pkgrel=1
pkgdesc="A free online multiplayer competitive FPS based on the Qfusion engine. This package applies a patch to fix fullscreen under Openbox."
url="http://www.warsow.net/"
license=('GPL')
arch=('i686' 'x86_64') 
depends=('curl' 'libjpeg' 'libvorbis' 'libxinerama' 'libxxf86dga' 
'libxxf86vm' 'sdl' 'warsow-data')
makedepends=('mesa' 'openal' 'unzip')
optdepends=('openal: for openal audio support')
conflicts=('warsow')
source=('warsow.desktop' 'warsow.launcher' 'wsw-server.launcher' 
'wswtv-server.launcher' 'warsowopenboxfs.patch' \
"warsow_${pkgver}_sdk.tar.gz::http://www.warsow.net:1337/~warsow/${pkgver}/warsow_${pkgver}_sdk.tar.gz")
noextract=("warsow_${pkgver}_sdk.zip")
md5sums=('f9bf60c80820237f7097c4e50a9582cd'
         'ec00081d81ad9802a8ca42fc2eac5498'
         'f73e10c26197178df71b941b10bf83d7'
         'd7e4a69835bbcf801e58307e9d6b951e'
         '9be36ccb2318f28fd782e6373b77ebcb'
         '288b510dde9249c29fbb1b4cb746306b')

build() {
  unset CFLAGS
	unset CXXFLAGS

  # Extract Game Source Code
  tar -xvf warsow_${pkgver}_sdk.tar.gz
  
  # Patch game for Openbox so fullscreen works
  cd $srcdir/warsow_${pkgver}_sdk/source/unix/
  cp ../../../../warsowopenboxfs.patch $srcdir/warsow_${pkgver}_sdk/source/unix/
  patch -p3 < warsowopenboxfs.patch

  # Compile Warsow
  cd $srcdir/warsow_${pkgver}_sdk/source/
  make -j1
}

package() {
  cd $srcdir/warsow_${pkgver}_sdk/source/
  
  # Create Destination Directories
  install -d $pkgdir/opt/warsow/

  # Move Compiled Data to Destination Directory
  cp -r $srcdir/warsow_${pkgver}_sdk/source/release/* \
      $pkgdir/opt/warsow

  # Install Client Game Launcher
  install -D -m 0755 $srcdir/warsow.launcher \
      $pkgdir/usr/bin/warsow

  # Install Server Game Launcher
  install -D -m 0755 $srcdir/wsw-server.launcher \
      $pkgdir/usr/bin/wsw-server

  # Install WSWTV Server Launcher
  install -D -m 0755 $srcdir/wswtv-server.launcher \
      $pkgdir/usr/bin/wswtv-server

  # Install Client Desktop Shortcut
  install -D -m 0644 $srcdir/warsow.desktop \
      $pkgdir/usr/share/applications/warsow.desktop

  # Install Icon
  install -D -m 0644 $srcdir/warsow_${pkgver}_sdk/source/win32/warsow.ico \
      $pkgdir/usr/share/pixmaps/warsow.ico
}

# vim: ts=2:sw=2
