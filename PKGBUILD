# Maintainer: Le_suisse <lesuisse.dev at gmail dot com>

pkgname=joliebulle-bzr
pkgver=313
pkgrel=1
pkgdesc="Brewing assistant and beer recipe design"
arch=('any')
url="https://launchpad.net/joliebulle"
license=('GPL3')
depends=('python' 'pyqt')
makedepends=('bzr')
provides=('joliebulle')
conflicts=('joliebulle')

_bzrtrunk=lp:joliebulle
_bzrmod=joliebulle

build() {
  cd "$srcdir"
  msg "Connecting to Bazaar server...."

  if [[ -d "$_bzrmod" ]]; then
    cd "$_bzrmod" && bzr pull "$_bzrtrunk" -r "$pkgver"
    msg "The local files are updated."
  else
    bzr branch "$_bzrtrunk" "$_bzrmod" -q -r "$pkgver"
  fi

  msg "Bazaar checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_bzrmod-build"
  cp -r "$srcdir/$_bzrmod" "$srcdir/$_bzrmod-build"
  #cd "$srcdir/$_bzrmod-build"

}

package() {
  cd "$srcdir/$_bzrmod-build/dist"
  python3 setup.py install --root="$pkgdir/" --optimize=1
}

