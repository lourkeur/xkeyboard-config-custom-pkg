# $Id$
# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=xkeyboard-config
pkgver=1.4
pkgrel=1
pkgdesc="X keyboard configuration files"
arch=(i686 x86_64)
license=('custom')
url="http://www.freedesktop.org/wiki/Software/XKeyboardConfig"
depends=('xorg-xkb-utils')
makedepends=('perlxml' 'pkgconfig')
provides=('xkbdata')
replaces=('xkbdata')
conflicts=('xkbdata')
source=(http://xlibs.freedesktop.org/xkbdesc/xkeyboard-config-${pkgver}.tar.bz2)
md5sums=('a9fe7efbc67a6966c4d4501f0cf88073')

build() {
  cd ${startdir}/src/${pkgname}-${pkgver}
  ./configure --prefix=/usr \
              --with-xkb-base=/usr/share/X11/xkb \
              --with-xkb-rules-symlink=xorg \
              --enable-compat-rules=yes || return 1
  make || return 1
  make DESTDIR=${startdir}/pkg install || return 1
  rm -f ${startdir}/pkg/usr/share/X11/xkb/compiled || return 1
  install -m755 -d ${startdir}/pkg/var/lib/xkb
  install -m755 -d ${startdir}/pkg/usr/share/licenses/${pkgname}
  install -m644 COPYING ${startdir}/pkg/usr/share/licenses/${pkgname}/ || return 1
}
