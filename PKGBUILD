# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=cef-minimal-obs
pkgver=127.1.11
_pkgcommit="g84246a3"
_chromiumver="127.0.6533.89"
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
sha512sums=('4bb2f151225aad985ea7dd2cc91c75c5e73f07676de078ae2e6832abf332602dcc06f2057e38dbddb4c6d4dd08be6b7d6ec4a158b3fb84c4fad0a6c1a689d304')

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
