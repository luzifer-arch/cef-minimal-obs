# Maintainer: Knut Ahlers <knut at ahlers dot me>

pkgname=cef-minimal-obs
pkgver=89.0.18
_pkgcommit="gb36241d"
_chromiumver="89.0.4389.114"
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
sha512sums=('28b2c7eb7e7de704fd1056cd192462d6b031922ef00e2d334fedad65513f7f81a687ee8cee5719984edee5352247ee39fd346c81ee5f84918b677497fca051bf')

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
