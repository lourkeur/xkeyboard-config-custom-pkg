srcname=xkeyboard-config
pkgname="${srcname}+custom"
pkgver=2.24
pkgrel=1
pkgdesc="X keyboard configuration files with custom layout added"
arch=(any)
license=('custom')
url="https://www.freedesktop.org/wiki/Software/XKeyboardConfig"
makedepends=('intltool' 'xorg-xkbcomp' 'libxslt' 'xorg-util-macros')
provides=("${srcname}")
conflicts=("${srcname}")
source=(https://xorg.freedesktop.org/archive/individual/data/${srcname}/${srcname}-${pkgver}.tar.bz2{,.sig})
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145')
validpgpkeys+=('15CFA5C595041D2CCBEA155F1732AA424A0E86B4') # "Sergey Udaltsov (For GNOME-related tasks) <svu@gnome.org>"
sha512sums=('96b65d18a85443a9bf93d65a4423da6e2b3d44882dae6a03bf46768a92017e9762cf3721361ba399c2873d53782944d0292eb673484f1cd8a8bdbf643e7a1dc0'
            'SKIP')

prepare() {
  cd ${srcname}-${pkgver}
  patch -uNp1 -i ../add_custom.patch
}

build() {
  cd ${srcname}-${pkgver}
  autoreconf
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
