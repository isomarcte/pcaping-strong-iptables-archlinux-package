# Maintainer: David Strawn <isomarcte@gmail.com>
pkgname=pcaping-strong-iptables
pkgver=3.0.0
pkgrel=1
pkgdesc='A packet capturing iptables based firewall.'
url="https://github.com/isomarcte/${pkgname}"
license=('BSD')
source=("https://github.com/isomarcte/${pkgname}/archive/${pkgver}.tar.gz")
md5sums=('bec6d74997e6912bb27b2860b523e199')
sha1sums=('0709a19467189db4ed3121bdba0499d904a518e8')
sha256sums=('e94cf017e8afa8463f0a7ef6b78265825af5229857bd4dacd382267771431c49')
sha384sums=('538749f60b939a33f927568300c47c6c383c9e5b85f0b44bd74874caa985cb683f8137ea8b395ecc1ea4d87c73c868af')
sha512sums=('e80efbbc476e3060c7788173e4aec3e95df948c56a95a488ff180f882139e6583d815656961a12eb843e79e5c2362a2fd7c85976362d78777a982718aa4b311d')
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
    local -r DESTDIR_PACKAGE="${pkgdir}/usr/share/pcaping-strong-iptables"
    local -r DESTDIR_SYSTEMD="${pkgdir}/usr/lib/systemd/system"
    local -r DESTDIR_USR_SBIN="${pkgdir}/usr/sbin"

    install -d "${DESTDIR_ETC}/iptables"

    mv "${DESTDIR_PACKAGE}/iptables.up.rules" "${DESTDIR_ETC}/iptables/iptables.rules"
    mv "${DESTDIR_PACKAGE}/ip6tables.up.rules" "${DESTDIR_ETC}/iptables/ip6tables.rules"
    rm -d "${DESTDIR_ETC}/iptables.up.rules.d"
    rm "${DESTDIR_PACKAGE}/iptables.down.rules" # Arch Linux daemon already handles this.
    rm "${pkgdir}/usr/lib/systemd/system/iptables.service" # Arch Linux already provides this.

    rm -r "${pkgdir}/usr/sbin"
    rm -r "${pkgdir}/usr/lib"
}
