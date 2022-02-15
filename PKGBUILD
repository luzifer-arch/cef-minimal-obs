# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=cef-minimal-obs
pkgver=95.7.10
_pkgcommit="g00d4ad5"
_chromiumver="95.0.4638.54"
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
sha512sums=('9a3184f73646c2388c0ce1a731325cd50dfbec48398a8f94a565324fb4b4cf35517de93db422aaf3cbeafb61fdb41b9a8fbba4da46b486ace168214af32b22cc')

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
