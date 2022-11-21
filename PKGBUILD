# Maintainer:  Anton Kudelin <kudelin at protonmail dot com>
# Contributor: Dimitris Kiziridis <ragouel at outlook dot com>
# Contributor: Joël Schaerer <joel.schaerer at laposte.net>
# Contributor: Ľubomir 'The_K' Kučera <lubomir.kucera.jr at gmail.com>
# Contributor: Robert Schwarz <mail@rschwarz.net>
# Contributor: Johannes Schlatow <johannes.schlatow@googlemail.com>
# Contributor: Stephan Friedrichs <deduktionstheorem@googlemail.com>

pkgname=scipoptsuite
pkgver=8.0.2
pkgrel=1
pkgdesc='Toolbox for generating and solving optimization problems (with Parallel Processing)'
arch=('x86_64')
url='https://scip.zib.de'
license=('LGPL3' 'custom:ZIB Academic License')
replaces=('ziboptsuite')
depends=('gmp' 'zlib' 'cppad' 'bliss' 'boost-libs' 'blas' 'gsl' 'tbb')
makedepends=('cmake' "${depends[@]}" 'boost')
optdepends=('cliquer: C routines for finding cliques in an arbitrary weighted graph'
            'hmetis: A set of programs for partitioning hypergraphs'
            'criterion: A cross-platform C and C++ unit testing framework')
provides=("scip=$pkgver"
          'soplex=6.0.2'
          'zimpl=3.5.3'
          'gcg=3.5.2'
          'papilo=2.1.1'
          'ipopt=3.13.2'
          'cppad=20180000.0'
          'zlib=1.2.11'
          'bliss=0.77'
          'gmp=6.2.1')
source=("local:///$pkgname-$pkgver.tgz")
sha256sums=('1cfc8d31b4ef9c12fae535f5c911616491439bb79cdfa39a30e4d035f4919d96')
options=('strip')

prepare(){
  mkdir -p "$srcdir/build"
}

build(){
  cd "$srcdir/build"
  cmake ../$pkgname-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DTPI=tny .. \
    -DIPOPT=OFF
  make
}

check() {
  cd "$srcdir/build"
  make check
}

package(){
  cd "$srcdir/build"
  make DESTDIR="$pkgdir" install
  install -Dm755 "$srcdir/$pkgname-$pkgver/scip/COPYING" \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  sed -i "180s|${srcdir}/${pkgname}-${pkgver}/build/zimpl/src/|usr/include|" \
    "$pkgdir/usr/include/zimpl/mmlparse2.h"
  sed -i "6s|${srcdir}||" "$pkgdir/usr/lib/cmake/gcg/gcg-config.cmake"
}
