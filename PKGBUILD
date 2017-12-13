# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Tomislav Ivek <tomislav.ivek@gmail.com>

pkgbase=python-distro
pkgname=('python-distro' 'python2-distro')
pkgver=1.1.0
pkgrel=1
pkgdesc='Linux OS platform information API'
url='https://github.com/nir0s/distro'
arch=('any')
license=('Apache')
makedepends=('python-setuptools' 'python-sphinx' 'python2-setuptools' 'python2-sphinx')
checkdepends=('python-pytest' 'python2-pytest')
options=('!makeflags')
source=(${pkgbase}-${pkgver}.tar.gz::https://github.com/nir0s/distro/archive/v${pkgver}.tar.gz)
sha256sums=('50bd749155f8823838a562cbfe7847880d64f05568dd8cca172546a371f243c5')
sha512sums=('eed2151674e0791c5bb37cde013c691e6421ef76f008c7ff8c50cc96812fc4ae0fd7428ea524e1229cd33f055ce6c89bf0de049a57477da017863308f88e4917')

prepare() {
  cp -a distro-${pkgver}{,-py2}

}

build() {
  (cd distro-${pkgver}
    python setup.py build
    make man SPHINXBUILD=sphinx-build
  )
  (cd distro-${pkgver}-py2
    python2 setup.py build
    make man SPHINXBUILD=sphinx-build2
  )
}

check() {
  (cd distro-${pkgver}
    py.test
  )
  (cd distro-${pkgver}-py2
    py.test2
  )
}

package_python-distro() {
  depends=('python' 'python-setuptools')
  cd distro-${pkgver}
  python setup.py install -O1 --root="${pkgdir}" --skip-build
  install -Dm 644 build_docs/man/ld.1 "${pkgdir}/usr/share/man/man1/${pkgname}.1"
  install -Dm 644 README.md CHANGES -t "${pkgdir}/usr/share/doc/${pkgname}"
}

package_python2-distro() {
  depends=('python2' 'python2-setuptools')
  cd distro-${pkgver}-py2
  python2 setup.py install -O1 --root="${pkgdir}" --skip-build
  install -Dm 644 build_docs/man/ld.1 "${pkgdir}/usr/share/man/man1/${pkgname}.1"
  install -Dm 644 README.md CHANGES -t "${pkgdir}/usr/share/doc/${pkgname}"
  mv "${pkgdir}/usr/bin/distro"{,2}
}

# vim: ts=2 sw=2 et:
