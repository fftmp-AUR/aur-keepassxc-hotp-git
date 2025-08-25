# Maintainer: fft

pkgname=keepassxc-hotp-git
pkgver=2.7.10
pkgrel=1
pkgdesc='keepassXC git version with patch to support HOTP and without supplement features'
arch=(x86_64)
url='https://keepassxc.org/'
license=('GPL-2.0-only OR GPL-3.0-only OR LGPL-2.1-only')
depends=(argon2 botan hicolor-icon-theme libxtst minizip qrencode qt5-svg qt5-x11extras)
makedepends=(git cmake ninja qt5-tools)
patch_url='https://github.com/fftmp/keepassxc/commit/'
source=('git+https://github.com/keepassxreboot/keepassxc.git#branch=develop'
        "p1.patch::${patch_url}/fb7b452573c40761ec6ac7eb727ecc5a6b05dabd.patch"
        "p2.patch::${patch_url}/71f19040484c52d2aaabdc6b7b459a0500a97273.patch"
        )
sha256sums=('SKIP' 'SKIP' 'SKIP')

provides=(keepassxc)

prepare() {
    patch --directory='keepassxc' -p1 --input='../p1.patch'
    patch --directory='keepassxc' -p1 --input='../p2.patch'
    mkdir -p build
}

build() {
    cd build
    cmake -G Ninja \
        ../keepassxc \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DWITH_TESTS=OFF \
        -DWITH_XC_UPDATECHECK=OFF \
        -DWITH_XC_DOCS=OFF \
        -DWITH_APP_BUNDLE=OFF
    ninja
}

package() {
    cd build
    DESTDIR="${pkgdir}" ninja install
}
