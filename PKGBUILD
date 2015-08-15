# Maintainer: Alain Kalker <a {dot} c {dot} kalker "at" gmail {dot} com>
pkgname=dparser
pkgver=1.30
pkgrel=1
pkgdesc="A scannerless GLR parser generator based on the Tomita algorithm"
arch=('i686' 'x86_64')
url="http://dparser.sourceforge.net/"
license=('BSD')
depends=('glibc' 'gc')
source=(http://prdownloads.sourceforge.net/$pkgname/d-$pkgver-src.tar.gz)
# bsdtar doesn't grok upstream tarball which has duplicate files in it
noextract=(d-$pkgver-src.tar.gz)
md5sums=('04b4e5ff4834d64e348deb294f655e7f')

build() {
  cd "$srcdir"
  # Need to extract source tarball with GNU tar
  tar xzf "d-$pkgver-src.tar.gz"
  cd "$srcdir/d"
  make D_USE_GC=1
}

package() {
  cd "$srcdir/d"
  make D_USE_GC=1 PREFIX="$pkgdir/usr" install
  install -d -m755 "$pkgdir/usr/share"
  mv "$pkgdir/usr/man" "$pkgdir/usr/share/"
  install -Dm644 COPYRIGHT "$pkgdir/usr/share/licenses/$pkgname/COPYRIGHT"
  install -Dm644 index.html "$pkgdir/usr/share/doc/$pkgname/index.html"
  cd "$srcdir"
  for f in \
      d/tests/ansic.test.g d/tests/python.test.g d/verilog/verilog.g \
      d/make_dparser.cat d/manual.html d/faq.html \
      d/dparse.h d/dparse_tables.h d/dsymtab.h; do
    install -Dm644 $f "$pkgdir/usr/share/doc/$pkgname/$f"
  done
}

# vim:set ts=2 sw=2 et:
