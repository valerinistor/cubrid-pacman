# Maintainer: Valeri Nistor <nistor.valeri@gmail.com>

pkgname=cubrid
pkgver=10.1.1
_buildver=7691-47d2437
pkgrel=1
pkgdesc='Comprehensive open source relational database management system highly optimized for Web Applications'
url='http://cubrid.org/'
arch=('x86_64')
license=('GPLv2')
depends=('ncurses5-compat-libs')
install=cubrid.install

source=(http://ftp.cubrid.org/CUBRID_Engine/${pkgver}/CUBRID-${pkgver}.${_buildver}-Linux.${arch}.tar.gz
        cubrid.service
        cubrid-database@.service
        cubrid.install
        cubrid.sh
        cubrid.csh)

md5sums=('f7a222cd606b7855d8dc000b2c24ea54'
         '7f4c8785860bfd9063da18caef2a6e2c'
         '226da8427bfc5d2d9ef6a734c9f00e71'
         '3ff4312587081bcc4fe3e5519bb74ca1'
         '7a366cc938717249b7cc0114ff98dfa3'
         '1de08824d0136935b1c4d1fadd4912d8')

package() {
    install -dm755 "$pkgdir/opt/${pkgname}"
    cp -R "$srcdir"/CUBRID/* "$pkgdir/opt/${pkgname}"

    # install profile.d script
    install -dm755 "${pkgdir}"/etc/profile.d
    install -m755 "${srcdir}"/cubrid.{csh,sh} "${pkgdir}"/etc/profile.d/

    # add cubrid service files
    install -Dm 644 "${srcdir}/${pkgname}.service" "${pkgdir}/usr/lib/systemd/system/${pkgname}.service"
    install -Dm 644 "${srcdir}/${pkgname}-database@.service" "${pkgdir}/usr/lib/systemd/system/${pkgname}-database@.service"

    # add cubrid library path to ld.so.conf.d
    install -d "${pkgdir}/etc/ld.so.conf.d"
    echo "/opt/${pkgname}/lib" > "${pkgdir}/etc/ld.so.conf.d/${pkgname}.conf"
}
