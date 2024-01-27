# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Danilo J. S. Bellini <danilo dot bellini at gmail dot com>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Morten Linderud <foxboron@archlinux.org>
# Contributor: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Contributor: Truocolo <truocolo@aol.com>

_py="python2"
_pkg="wheel"
pkgname="${_py}-wheel"
pkgver=0.37.1
pkgrel=5
pkgdesc="A built-package format for Python, version for Python 2.7"
arch=(
  any
)
url="https://github.com/pypa/wheel"
license=(
  'MIT'
)
depends=(
  'python2'
)
makedepends=(
  'python2-setuptools'
)
checkdepends=(
  'python2-pytest'
)
source=(
  "$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz"
)
sha256sums=(
  'a82516a039e521100ecdef137f9e44249bf6903f9aff7d368e84ac31d60597f5'
)

prepare() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  sed \
    -i \
    's/_.name/&.lower()/' \
    "src/${_pkg}/${_pkg}file.py"

  # Make python2-pytest-cov
  # no longer a requirement
  sed \
    -i \
    /-cov/d \
    setup.cfg
}

build() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      build
  "${_py}" \
    setup.py \
      egg_info
}

check() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  PYTHONPATH="${PWD}/src" \
    "${_py}" \
      -m \
        pytest \
      -W \
        ignore::DeprecationWarning
}

package() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
	--optimize=1 \
	--skip-build
  install \
    -Dm644 \
    LICENSE.txt \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"
  mv \
    "${pkgdir}/usr/bin/wheel" \
    "${pkgdir}/usr/bin/wheel2"
}

# vim:set sw=2 sts=-1 et:
