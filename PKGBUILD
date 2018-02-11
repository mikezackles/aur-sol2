# Maintainer: mikezackles <mikezackles@gmail.com>
_basename="sol2"
pkgname=${_basename}-git
pkgver=v2.19.0.r113.1d0683a
pkgrel=1
pkgdesc='A C++ <-> Lua API wrapper with advanced features and top-notch performance'
arch=('x86_64')
url="https://github.com/ThePhD/sol2"
license=('MIT')
makedepends=('git' 'cmake>=3.0.0')
provides=(${_basename}=${pkgver})
conflicts=(${_basename})
source=(${_basename}::git://github.com/ThePhD/sol2.git)
md5sums=('SKIP')

pkgver() {
	cd "${srcdir}/${_basename}"
	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}

build() {
  cd "${srcdir}/${_basename}"

  if [[ -d build ]]; then
      rm -rf build
  fi
  mkdir build && cd build

  cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX="/usr"
  make
}

package() {
  cd "${srcdir}/${_basename}/build"
  make install DESTDIR="${pkgdir}/"

  install  -D -m644 "${srcdir}/${_basename}/README.md" \
           "${pkgdir}/usr/share/doc/${_basename}/README"

  install  -D -m644 "${srcdir}/${_basename}/LICENSE.txt" \
           "${pkgdir}/usr/share/licenses/${_basename}/LICENSE"
}
