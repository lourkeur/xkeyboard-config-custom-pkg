srcname=xkeyboard-config
pkgname="${srcname}+custom"
pkgver=2.26
pkgrel=1
pkgdesc="X keyboard configuration files with custom layout added"
arch=(any)
license=('custom')
url="https://www.freedesktop.org/wiki/Software/XKeyboardConfig"
makedepends=('intltool' 'xorg-xkbcomp' 'libxslt')
provides=("${srcname}")
conflicts=("${srcname}")
source=(https://xorg.freedesktop.org/archive/individual/data/${srcname}/${srcname}-${pkgver}.tar.bz2{,.sig}
        pt-layout.patch)
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145')
validpgpkeys+=('15CFA5C595041D2CCBEA155F1732AA424A0E86B4') # "Sergey Udaltsov (For GNOME-related tasks) <svu@gnome.org>"
sha512sums=('5c8a31f7a6ad5daed8a3fceb56230b2e2fc04a25f52a43b3b4ea81e4a6ab15c52869f749c4b747d855cd4b618c04bcbb40e85dec7eab31fbe3bd45e8c9b755ef'
            'SKIP'
            '98c8b47e9a36ba3f130454fdd68c508f54b78eb65ddb071ca85bdcc3b324699e51155e3fc425ccae98350bb6430fea4771c0338024c1e06063a54b879bb707db')

prepare() {
  cd ${srcname}-${pkgver}
  patch -uNp1 -i ../add_custom.patch
  # fix broken pt layout - FS#61634
  patch -Np1 -i ../pt-layout.patch
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
