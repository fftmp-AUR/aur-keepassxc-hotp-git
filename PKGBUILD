# Maintainer: fft

pkgname=keepassxc-hotp-git
pkgver=2.7.9
pkgrel=2
pkgdesc="keepassXC git version with patch to support HOTP and without supplement features"
arch=(x86_64)
url="https://keepassxc.org/"
license=('GPL-2.0-only OR GPL-3.0-only OR LGPL-2.1-only')
depends=(botan hicolor-icon-theme libxtst minizip qrencode qt5-svg qt5-x11extras)
makedepends=(git intltool cmake qt5-tools)
patch_url='https://github.com/fftmp/keepassxc/commit/'
source=('git+https://github.com/keepassxreboot/keepassxc.git#branch=develop'
        "p1.patch::${patch_url}/1c802f5e55d76f94c5a2e9e2e806216094e30b2a.patch"
        "p2.patch::${patch_url}/6daced8fa038957af8719b9e5dc4ee0324982467.patch"
        )
sha256sums=('SKIP' 'SKIP' 'SKIP')

prepare() {
    patch --directory="keepassxc" -p1 --input='../p1.patch'
    patch --directory="keepassxc" -p1 --input='../p2.patch'
    mkdir -p build
}

build() {
    cd build
    cmake ../keepassxc \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DWITH_TESTS=OFF \
        -DWITH_XC_UPDATECHECK=OFF \
        -DWITH_XC_DOCS=OFF \
        -DWITH_APP_BUNDLE=OFF
    make
}

package() {
    cd build
    make DESTDIR="$pkgdir" install
}
