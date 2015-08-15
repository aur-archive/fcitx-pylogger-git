# Maintainer: Yichao Yu <yyc1992 AT gmail.com>
# Contributor: Yichao Yu <yyc1992 AT gmail.com>

pkgname=fcitx-pylogger-git
pkgver=20121029
pkgrel=1
pkgdesc="PinYin Logger for Fcitx"
arch=("i686" "x86_64")
license=('GPL')
url="http://fcitx-im.org/wiki/Fcitx"
depends=('fcitx-git')
makedepends=('git' 'cmake')
conflicts=('fcitx-pylogger')
provides=('fcitx-pylogger')

_gitname="fcitx-pylogger"
_gitroot="https://github.com/yuyichao/fcitx-pylogger.git"

build() {
  cd "$srcdir"
  msg "Connecting to the GIT server...."

  if [[ -d $srcdir/$_gitname ]] ; then
    cd $_gitname
    git checkout master
    git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  cd "$srcdir/$_gitname"
  git pull

  msg "Creating make environment..."

  mkdir -p "$srcdir/$_gitname-build"

  msg "Starting make..."
  cd "$srcdir/$_gitname-build"
  cmake ../$_gitname -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
  make
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir" install
}
