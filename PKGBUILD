# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Tomislav Ivek <tomislav.ivek@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=distro
pkgname="${_py}-${_pkg}"
pkgver=1.9.0
pkgrel=2
pkgdesc='Linux OS platform information API'
_http="https://github.com"
_ns="${pkgname}"
url="${_http}/${_ns}/${_pkg}"
arch=(
  'any'
)
license=(
  'Apache-2.0'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-sphinx"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
  "${_py}-setuptools"
)
checkdepends=(
  "${_py}-pytest"
)
options=(
  '!makeflags'
)
source=(
  "${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  '9ed033e9fb0a5a531a93d85d8d3c0afb67ec009b851146c76f819617cc13b28a6e6dc412899690baec2aa57d57389a347968c649eb99fefa6f782340166f83c4'
)
b2sums=(
  'e50d91a9eba711a8196a6a8bb078c5d8611955fd042dea398aa40db238bbabda55e09d142dd95c769d4e7032425412eb1bacede67053d3e5f1c3892d998c0a20'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  PYTHONPATH="build/lib" \
  pytest
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    README.md \
    CHANGELOG.md \
    -t \
    "${pkgdir}/usr/share/doc/${pkgname}"
}

# vim: ts=2 sw=2 et:
