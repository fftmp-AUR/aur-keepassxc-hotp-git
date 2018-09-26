# Maintainer: fft

pkgname=keepassxc-hotp-git
pkgver=2.7.4
pkgrel=1
pkgdesc="keepassXC git version with patch to support HOTP and without supplement features"
arch=(x86_64)
url="https://keepassxc.org/"
license=(GPL)
depends=(botan hicolor-icon-theme libxtst qrencode qt5-svg qt5-x11extras)
makedepends=(git intltool cmake qt5-tools)
source=('git+https://github.com/keepassxreboot/keepassxc.git#branch=develop'
        'https://github.com/fftmp/keepassxc/commit/aa1e6f67d295fd062db57623657bfb004bd7bcda.patch')
sha256sums=('SKIP' '5cb0e78b2f6ae1aea325bd3f29c0e1924e8ceba807514187a2d38765277b9f1e')

prepare() {
    patch --directory="keepassxc" -p1 --input='../aa1e6f67d295fd062db57623657bfb004bd7bcda.patch'
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
