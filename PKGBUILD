# Previous maintainer: Andrew Krasichkov <buglloc _ at _ yandex _ dot _ru>

pkgname=brick-git-artalus
pkgver=develop
pkgrel=1
pkgdesc="An open source Bitrix24 messenger client"
arch=('i686' 'x86_64')
url="https://github.com/buglloc/brick"
license=("MIT")
depends=("alsa-lib" "desktop-file-utils" "gconf" "libxtst" "libxss" "xdg-utils" "gtk2" "libnotify" "nss")
optdepends=("libappindicator-gtk2: modern system indicator support for KDE5, Cinnamon, Unity, etc")
conflicts=("brick")
makedepends=("cmake")
install=${pkgname}.install
source=("https://github.com/Artalus/brick/archive/${pkgver}.tar.gz")
sha256sums=(SKIP)

build() {
  if [ -z $BRICK_AUR ]; then
    printf '\033[1;31m'
    echo "! THIS IS A TEST VERSION OF A PACKAGE !"
    echo "! PLEASE make sure you know why you are using it, and THEN defnie 'BRICK_AUR=1' envvar !"
    printf '\033[0m'
    exit 1
  fi

  cd ${srcdir}
  mkdir -p out
  cd out
  cmake -DCMAKE_INSTALL_PREFIX=${pkgdir} -DSKIP_BRICK_REGISTER=1 "../brick-${pkgver}"
  make
}

package() {
  cd ${srcdir}/out
  make install
  install -dm755 "${pkgdir}/usr/bin"
  rm "${pkgdir}/usr/bin/brick" # TODO: handle this in CMake itself?
  ln -sf /opt/brick/brick "${pkgdir}/usr/bin/brick-chat"
  ln -sf /opt/brick/bin/brick-client "${pkgdir}/usr/bin/brick-client"
}
