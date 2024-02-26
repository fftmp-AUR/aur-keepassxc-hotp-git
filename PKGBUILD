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
        'https://github.com/fftmp/keepassxc/commit/9b24dac077971dc1517ea4b37d6dd1adcce71bfa.patch'
        'https://github.com/fftmp/keepassxc/commit/dcf0fc98684d7081886784efa0afc8070ff2d012.patch'
        )
sha256sums=('SKIP'
			'eee52115e3d61d61c4828726256749c59e8cd2d8d75643bb274b28a63a766f83'
			'fa3750db8efa188fb0761ed5cd1e6d357f4abb5bbe0d3499fcc1907e55124b4b'
)

prepare() {
    patch --directory="keepassxc" -p1 --input='../9b24dac077971dc1517ea4b37d6dd1adcce71bfa.patch'
    patch --directory="keepassxc" -p1 --input='../dcf0fc98684d7081886784efa0afc8070ff2d012.patch'
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
