# Maintainer: kevku <kevku@gmx.com>
pkgname=libdigidoc-svn
pkgver=3575
pkgrel=1
pkgdesc="C Library for digidoc.sk.ee client (Community dev version)"
arch=('x86_64' 'i686')
url="http://code.google.com/p/esteid"
license=('LGPL')
depends=('opensc' 'libxml2')
makedepends=('cmake' 'subversion')
conflicts=('sk-libdigidoc-svn')

_svntrunk=https://esteid.googlecode.com/svn/${pkgname%-svn}/trunk
_svnmod=${pkgname%-svn}

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  cmake . -DCMAKE_INSTALL_PREFIX=/usr -DLIB_SUFFIX="" -DSYSCONF_INSTALL_DIR=/etc
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}
