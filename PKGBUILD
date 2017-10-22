# Maintainer: David Strawn <isomarcte@gmail.com>
pkgname=pcaping-strong-iptables
pkgver=2.2.0
pkgrel=1
pkgdesc='A packet capturing iptables based firewall.'
url="https://github.com/isomarcte/${pkgname}"
license=('BSD')
source=("https://github.com/isomarcte/${pkgname}/archive/${pkgver}.tar.gz")
md5sums=('9b9d680f72bc8504f206512e8766885d')
sha1sums=('2e120f8e63f18790f1c8f19cfb4f769b1ff3df5f')
sha256sums=('a925537c8826b66659413f5b7df0b39d319240aca749a0b56d6b4c74c7664e46')
sha384sums=('70c962046b85aff668f6394a12d0e7916855eae037e4ed159e24c93efe9117bfa94f7f9f73525069317c35aad4576824')
sha512sums=('f53b5dfb3bdaaa2e1cbf5eac10bcd96502817c527ef438f6838192f6b16f17b3d4298ad35cfc5251704be025ee38c8c27b723817811b3351ebaf113dd181914b')
arch=('any')
depends=('iptables'
         'systemd')
optdepends=('libpcap'
            'ulogd'
            'logrotate')
makedepends=('make')
backup=('etc/iptables/iptables.rules')
install="${pkgname}.install"

package() {
    cd "$pkgname-$pkgver"

    local -r LICENSE_DIR="$pkgdir/usr/share/licenses/$pkgname/"

    install -d "$LICENSE_DIR"
    install -t "$LICENSE_DIR" LICENSE

    make DESTDIR="$pkgdir" install

    # Fix the file location for Arch Linux

    local -r DESTDIR_ETC="${pkgdir}/etc"
    local -r DESTDIR_SYSTEMD="${pkgdir}/usr/lib/systemd/system"
    local -r DESTDIR_USR_SBIN="${pkgdir}/usr/sbin"

    install -d "${DESTDIR_ETC}/iptables"

    mv "${DESTDIR_ETC}/iptables.up.rules" "${DESTDIR_ETC}/iptables/iptables.rules"
    rm -d "${DESTDIR_ETC}/iptables.up.rules.d"
    rm "${DESTDIR_ETC}/iptables.down.rules" # Arch Linux daemon already handles this.
    rm "${pkgdir}/usr/lib/systemd/system/iptables.service" # Arch Linux already provides this.
    rm -r "${pkgdir}/usr/sbin"
    rm -r "${pkgdir}/usr/lib"
}
