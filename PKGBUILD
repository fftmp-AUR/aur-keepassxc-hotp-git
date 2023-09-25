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
        'https://github.com/fftmp/keepassxc/commit/07fe978b34e0ca8e809b1d967a7263e993741cb5.patch'
        'https://github.com/fftmp/keepassxc/commit/4817d8c672164bc1fe022168e5b84d84ac06437b.patch')
sha256sums=('SKIP' '1fbff34ebc2cade98b19f9efcf8510586fa1b48e95ba0d08d659c4e5637fb8d3' 'da2c1deb190a6892192defcc1aa5f3f6ae859d5b92f087fedd964140dbfc783c')

prepare() {
    patch --directory="keepassxc" -p1 --input='../07fe978b34e0ca8e809b1d967a7263e993741cb5.patch'
    patch --directory="keepassxc" -p1 --input='../4817d8c672164bc1fe022168e5b84d84ac06437b.patch'
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
