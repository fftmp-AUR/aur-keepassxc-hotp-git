# Maintainer: fft

pkgname=keepassxc-hotp-git
pkgver=2.7.9
pkgrel=1
pkgdesc="keepassXC git version with patch to support HOTP and without supplement features"
arch=(x86_64)
url="https://keepassxc.org/"
license=('GPL-2.0-only OR GPL-3.0-only OR LGPL-2.1-only')
depends=(argon2 botan hicolor-icon-theme libxtst minizip qrencode qt5-svg qt5-x11extras)
makedepends=(git intltool cmake qt5-tools)
patch_url='https://github.com/fftmp/keepassxc/commit/'
source=('git+https://github.com/keepassxreboot/keepassxc.git#branch=develop'
        "p1.patch::${patch_url}/b77c117ea52989f4b3ee6b259229a22b4edbe692.patch"
        "p2.patch::${patch_url}/7a6c2d962a50fc693617b9645d461447bc293952.patch"
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
