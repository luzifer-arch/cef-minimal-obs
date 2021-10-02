# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=cef-minimal-obs
pkgver=90.6.7
_pkgcommit="g19ba721"
_chromiumver="90.0.4430.212"
pkgrel=1
pkgdesc="Chromium Embedded Framework minimal release"
arch=("x86_64")
url="https://bitbucket.org/chromiumembedded/cef"
license=("BSD")
depends=("nss" "alsa-lib" "libxss" "libxtst" "libglvnd" "pango" "libxcursor" "dbus" "libxrandr" "libxcomposite" "at-spi2-atk")
makedepends=("cmake" "make")
provides=('cef')
conflicts=('cef-standard' 'cef-git' 'cef-minimal')

_cdn_build_package_url="https://cef-builds.spotifycdn.com"
_pkgver="${pkgver}+${_pkgcommit}+chromium-${_chromiumver}"
_url_pkgver="${pkgver}%2B${_pkgcommit}%2Bchromium-${_chromiumver}"

source=("${_cdn_build_package_url}/cef_binary_${_url_pkgver}_linux64_minimal.tar.bz2")
sha512sums=('e9149dc8dfa137c5955d245444c1be82332b2bbd5128ae0cb2fe6844081df3c4720a5bb9093076e02588543a90b2b81f574abb9bd8e2ccafacc352cb76d4f982')

build() {
	cd "$srcdir"/cef_binary_${_pkgver}_linux64_minimal
	sed -i 's/-Werror/#-Werror/g' cmake/cef_variables.cmake
	cmake .
	make libcef_dll_wrapper
}

package() {
	mkdir -p "$pkgdir"/opt/cef/
	cp -R "$srcdir"/cef_binary_${_pkgver}_linux64_minimal/* "$pkgdir"/opt/cef
	install -Dm644 "$srcdir"/cef_binary_${_pkgver}_linux64_minimal/LICENSE.txt "$pkgdir"/usr/share/licenses/${pkgname}/LICENSE

	# Fix read permissions
	chmod 644 "$pkgdir"/opt/cef/libcef_dll_wrapper/libcef_dll_wrapper.a
}
