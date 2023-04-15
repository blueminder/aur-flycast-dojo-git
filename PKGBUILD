# Maintainer: Enrique Santos <me@eos.fyi>

_pkgname=flycast-dojo
pkgname=$_pkgname-git
pkgver=r6794.aaa968192
pkgrel=1
pkgdesc='A fork of Flycast, a multiplatform Sega Dreamcast, Naomi and Atomiswave emulator. Intended for netplay, game training, and online tournament play.'
arch=('x86_64')
url="https://github.com/blueminder/flycast-dojo"
license=('GPL2')
depends=('libgl' 'libzip' 'xxhash' 'zlib' 'alsa-lib')
makedepends=('git' 'cmake' 'python' 'systemd' 'asio')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("${_pkgname}::git+$url.git")
md5sums=('SKIP')

pkgver() {
  cd $_pkgname
  git describe --long --tags --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd $_pkgname
	git submodule update --init --recursive
}

pkgver() {
	cd $_pkgname
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cmake -B build -S $_pkgname \
		-DCMAKE_INSTALL_PREFIX='/usr'
	make -C build
}

package() {
	install -Dm755 build/$_pkgname "$pkgdir"/usr/bin/$_pkgname
	cd $_pkgname/shell/linux
	install -Dm644 $_pkgname.png "$pkgdir"/usr/share/pixmaps/$_pkgname.png
	install -Dm644 $_pkgname.desktop "$pkgdir"/usr/share/applications/$_pkgname.desktop
}

