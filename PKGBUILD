srcname=xkeyboard-config
pkgname="${srcname}+custom"
pkgver=2.20
pkgrel=1
pkgdesc="X keyboard configuration files with custom layout added"
arch=(any)
license=('custom')
url="https://www.freedesktop.org/wiki/Software/XKeyboardConfig"
makedepends=('intltool' 'xorg-xkbcomp' 'libxslt')
provides=("${srcname}")
conflicts=("${srcname}")
source=(https://xorg.freedesktop.org/archive/individual/data/${srcname}/${srcname}-${pkgver}.tar.bz2{,.sig})
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145')
sha256sums=('d1bfc72553c4e3ef1cd6f13eec0488cf940498b612ab8a0b362e7090c94bc134'
            'SKIP')

prepare() {
  cd ${srcname}-${pkgver}
  patch -uNp1 -i ../add_custom.patch
}

build() {
  cd ${srcname}-${pkgver}
  ./configure --prefix=/usr \
      --with-xkb-base=/usr/share/X11/xkb \
      --with-xkb-rules-symlink=xorg \
      --enable-compat-rules=yes
  make
 }
 
 package() { 
  cd ${srcname}-${pkgver}

  make DESTDIR="${pkgdir}" install
  rm -f "${pkgdir}/usr/share/X11/xkb/compiled"

  install -m755 -d "${pkgdir}/var/lib/xkb"
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"
}
