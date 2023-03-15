# Maintainer: Atom Long <atom.long@hotmail.com>

pkgname=jq
pkgver=1.6
pkgrel=1
pkgdesc="Command-line JSON processor (msys2)"
arch=(any)
url='https://stedolan.github.io/jq/'
license=('MIT')
makedepends=("autotools" "gcc")
depends=("gcc-libs"
         "oniguruma")
source=("https://github.com/stedolan/${pkgname}/releases/download/${pkgname}-${pkgver}/${pkgname}-${pkgver}.tar.gz"
        no-undefined.patch)
sha256sums=('5de8c8e29aaa3fb9cc6b47bb27299f271354ebb72514e3accadc7d38b5bbaa72'
            'ed3f9824901a49d146b74c2a0a212595522dfa0fa5da32200c8384a779bbfa78')
noextract=(${pkgname}-${pkgver}.tar.gz)

prepare() {
  tar -xzvf ${srcdir}/${pkgname}-${pkgver}.tar.gz -C ${srcdir} || true

  cd "${srcdir}"/${pkgname}-${pkgver}
  cp README.md README
  patch -p1 -i ${srcdir}/no-undefined.patch

  autoreconf -fiv
}

build() {
  cd "${srcdir}"/${pkgname}-${pkgver}
  ../${pkgname}-${pkgver}/configure \
    --enable-static \
    --enable-shared \
    --disable-docs

  make
}

check() {
  cd "${srcdir}"/${pkgname}-${pkgver}
  make check || true
}

package() {
  cd "${srcdir}"/${pkgname}-${pkgver}
  make install DESTDIR="${pkgdir}"
}
