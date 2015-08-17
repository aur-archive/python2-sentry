# Maintainer: Benjamin A. Shelton <zancarius@gmail.com>
# Source: https://github.com/zancarius/archlinux-pkgbuilds

## !!! WARNING, PLEASE READ !!! ##
#
# python2-sentry will be RENAMED to sentry as per the Arch
# Python packaging guidelines since this is an application and
# not a library:
# https://wiki.archlinux.org/index.php/Python_Package_Guidelines
#
# Please install the package "sentry" instead.
#
# I will continue maintaining this package for a few update
# cycles until February 1st, 2013, at which point this package
# will most likely be merged into sentry.

pkgname=python2-sentry
pkgver=5.4.5
pkgrel=1
pkgdesc="Python-based realtime logging and aggregation server."
arch=(any)
url="http://pypi.python.org/pypi/sentry"
license=(BSD)
depends=(
    python2
)
makedepends=(git python2-distribute python2-virtualenv)
options=(!strip)
install="${pkgname}.install"
source=(
    "http://pypi.python.org/packages/source/s/sentry/sentry-${pkgver}.tar.gz"
    "sentry.install"
    "sentry.service"
)
md5sums=(
    8c92260cc2b956edf8340b5634ba0b08 # sentry tarball
    2c5f9de8bdc07895b765bb62a3aff7b4 # sentry.install
    7d90b474e728204d8954301440ac5d53 # sentry.service
)

_pkgname=sentry

build () {


    mkdir -p "${pkgdir}/opt/sentry"
    virtualenv2 "${pkgdir}/opt/sentry"

    "${pkgdir}/opt/sentry/bin/pip" install mysql-python
    "${pkgdir}/opt/sentry/bin/pip" install psycopg2

    cd "${srcdir}/${_pkgname}-${pkgver}"
    "${pkgdir}/opt/sentry/bin/python2" setup.py install --optimize=1

    # Remove Desktop Services Store from package. This has been removed
    # from django-paging's Github repo but still persists in the PIP
    # package. Harmless, but I don't like them. :) More information:
    # http://en.wikipedia.org/wiki/.DS_Store
    find "${pkgdir}" -name '.DS_Store' -delete

}

package () {

    install -Dm0644 "${srcdir}/${_pkgname}-${pkgver}/LICENSE" "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
    install -Dm0644 "${srcdir}/${_pkgname}.service" "${pkgdir}/usr/lib/systemd/system/sentry.service"

}
