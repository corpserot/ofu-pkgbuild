# Maintainer: Steven! Ragnarök <steven@nuclearsandwich.com>
pkgname=oils-for-unix
pkgver=0.18.0
pkgrel=1
pkgdesc="A collection of Unix shells and utilities."
arch=('x86_64')
url="https://www.oilshell.org"
license=('Apache-2.0')
depends=(readline)
install=oils.install
makedepends=(bash readline tar)
source=("https://www.oilshell.org/download/${pkgname}-${pkgver}.tar.gz")
sha256sums=('f5177ab35bb425f635b90e720b24b269f7a3915ca193f52c3e6223a02d0683f9')
noextract=("${pkgname}-${pkgver}.tar.gz")

prepare() {
	# https://github.com/oilshell/oil/issues/1731
	# TODO upstream should have fixed this already, where GNU tar is then not needed
	tar -xf "${pkgname}-${pkgver}.tar.gz"
}

build() {
	cd "$pkgname-$pkgver"
	./configure --prefix=/usr
	# If the current working directory (.) is on your PATH, then this takes
	# precedence over the `install` utility and creates a recursive call to
	# itself.
	mv install install-ofu
	_build/oils.sh
}

check() {
	cd "$pkgname-$pkgver"

	# ad-hoc testing
	./_bin/cxx-opt-sh/osh -c 'echo hi >/dev/null'
	./_bin/cxx-opt-sh/osh -n -c 'echo hi >/dev/null'
}

package() {
	cd "$pkgname-$pkgver"
	DESTDIR="$pkgdir" sh -x ./install-ofu
}
