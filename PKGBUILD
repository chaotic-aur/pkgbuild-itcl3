# Maintainer: Piotr Rogoża <rogoza dot piotr at gmail dot com>
# Contributor: Nick B <Shirakawasuna at gmail _dot_com>
# vim:set ts=2 sw=2 et ft=sh tw=100: expandtab

pkgname=itcl3
pkgver=3.4.3
pkgrel=1
pkgdesc="Provides the extra language support needed to build large Tcl/Tk applications, version 3.4"
arch=('i686' 'x86_64')
url="http://incrtcl.sourceforge.net/"
license=('custom')
depends=('glibc' 'tcl')
provides=(itcl)
conflicts=(itcl)
source=("https://downloads.sourceforge.net/project/incrtcl/%5BIncr%20Tcl_Tk%5D-source/Itcl%20$pkgver/itcl$pkgver.tar.gz")

prepare() {
  cd "$srcdir"/itcl$pkgver
  sed -ri 's,\$\(INSTALL_DATA\) itclConfig\.sh \$\(DESTDIR\)\$\(libdir\),$(INSTALL_DATA) itclConfig.sh $(DESTDIR)$(pkglibdir),' Makefile.in
  sed -ri 's,(itcl_.*?)`pwd`,\1/usr/lib/itcl'${pkgver%.*}, configure
}

build() {
  cd "$srcdir"/itcl$pkgver

  if [ `uname -m` = "x86_64" ]; then
    ./configure --prefix=/usr --enable-64bit
  else
    ./configure --prefix=/usr
  fi
  make all
}

package(){
  cd "$srcdir"/itcl$pkgver

  make DESTDIR="$pkgdir/" install
  install -Dm644 license.terms "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  chmod 644 "$pkgdir"/usr/lib/itcl${pkgver%.*}/libitclstub${pkgver%.*}.a
  
  # conflict with tcl-8.6.0
  rm -rf "$pkgdir"/usr/include
  rm -rf "$pkgdir"/usr/share/man

  #cleaning
  rmdir "$pkgdir"/usr/bin
}
md5sums=('bea70fc6e6a3fb049fdada405161b934')
