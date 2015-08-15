# Maintainer: Jaroslav Supolik <kadzi@centrum.cz>
# Contributor: Jon Gjengset <jon@tsp.io>
# Contributor: Gaetan Bisson <bisson@archlinux.org>
# Based on Gaetan's corsix-th package in the AUR

pkgname=corsix-th-git
pkgver=0.40.r209.g582fee0
pkgrel=1
pkgdesc='Reimplementation of the game engine of Theme Hospital'
url='https://github.com/CorsixTH/CorsixTH/'
arch=('i686' 'x86_64' 'armv7h')
license=('MIT')
makedepends=('cmake' 'git')
conflicts=('corsix-th')
depends=('sdl2_mixer' 'ffmpeg' 'timidity++' 'luajit' 'lua51-filesystem' 'lua51-lpeg')
optdepends=("freetype2: font support beyond the original game's bitmap fonts"
            "timidity-freepats: original background music playback")
source=("git+https://github.com/CorsixTH/CorsixTH.git"
        'bin')
sha1sums=('SKIP'
          '7fd6ae8db366b7f9c4671708e8ea7beb48f1bea3')

# If you do not have a copy of Theme Hospital,
# you can download the data files of the demo:
#   http://th.corsix.org/Demo.zip

pkgver() {
#	cd "$pkgname"
	cd "$srcdir/CorsixTH"
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "${srcdir}/CorsixTH"
	# work around broken 3.0 cmake config
	ln -sfn ../LICENSE.txt CorsixTH/LICENSE.txt
}

build() {
	cd "${srcdir}/CorsixTH"
		cmake \
		-D LUA_INCLUDE_DIR=/usr/include/luajit-2.0 \
		-D LUA_LIBRARY=/usr/lib/libluajit-5.1.so \
		-D CMAKE_INSTALL_PREFIX=/usr/share/ \
		-D CMAKE_BUILD_TYPE=Release \
		-Wno-dev .
	cd CorsixTH
	make
}

package() {
	cd "${srcdir}/CorsixTH/CorsixTH"
	make DESTDIR="${pkgdir}" install
	install -Dm755 ../../bin "${pkgdir}/usr/bin/CorsixTH"
	install -Dm644 LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -Dm644 ../DebianPackage/usr/share/applications/CorsixTH.desktop "${pkgdir}/usr/share/applications/CorsixTH.desktop"
	sed -e 's/games/share/g' -i "${pkgdir}/usr/share/applications/CorsixTH.desktop"

}
