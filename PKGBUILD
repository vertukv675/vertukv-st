_pkgname=st
pkgname=${_pkgname}-vertukv-git
pkgver=0.9.r228.13f2b13
pkgrel=1
pkgdesc='vertukv st build'
url=https://github.com/vertukv675/vertukv-st
arch=(any)
license=(MIT)
makedepends=(ncurses libxext git)
depends=(libxft ttf-jetbrains-mono)
provides=("${_pkgname}")
conflicts=("${_pkgname}")
source=("${pkgname}::git+${url}.git")
sha256sums=('SKIP')

pkgver() {
	cd "${pkgname}"
	echo "$(awk '/^VERSION =/ {print $3}' config.mk).r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {
	cd "${pkgname}"
	{
		echo "CPPFLAGS+=${CPPFLAGS}"
		echo "CFLAGS+=${CFLAGS}"
		echo "LDFLAGS+=${LDFLAGS}"
	} >>config.mk
	# skip terminfo which conflicts with ncurses
	sed -i '/tic /d' Makefile
}

build() {
	cd "${pkgname}"
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd "${pkgname}"
	make PREFIX=/usr DESTDIR="${pkgdir}" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
