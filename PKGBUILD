# Maintainer: fft

pkgname=keepassxc-hotp-git
pkgver=2.7.9
pkgrel=1
pkgdesc="keepassXC git version with patch to support HOTP and without supplement features"
arch=(x86_64)
url="https://keepassxc.org/"
license=(GPL)
depends=(botan hicolor-icon-theme libxtst qrencode qt5-svg qt5-x11extras)
makedepends=(git intltool cmake qt5-tools)
patch_url='https://github.com/fftmp/keepassxc/commit/'
source=('git+https://github.com/keepassxreboot/keepassxc.git#branch=develop'
        "p1.patch::${patch_url}/5ae7a9190f878610ed7f55a737cef3776f46f3ff.patch"
        "p2.patch::${patch_url}/15e95d0b0fa4defdfce1bdf3d0afb6657a8fe055.patch"
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
