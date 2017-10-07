# Maintainer: David Strawn <isomarcte@gmail.com>
pkgname=pcaping-strong-iptables
pkgver=2.1.1
pkgrel=1
pkgdesc='A packet capturing iptables based firewall.'
url="https://github.com/isomarcte/${pkgname}"
license=('BSD')
source=("https://github.com/isomarcte/${pkgname}/archive/${pkgver}.tar.gz")
md5sums=('6dcec8a29b661fc95fe0df32537d5373')
sha1sums=('c85e2215cc7dd3bd215ad056458410dabe337fe9')
sha256sums=('9d2fd0411c9bef37af3fac42aab14ab7daeb46701e1b35e205fea1049de087e4')
sha384sums=('3a4a6cd3619032094de971e08dcbb1f6c06ab5c55d6c6651e7845a78533fa42d6c5405af777d10cf3e8073b146a3c93d')
sha512sums=('2aff417efd1483eabb68c265e204fb33362909978c895a8f46126ddc0b8e1be7ef070b85005c2084cdb7ee503572c0cf429dc1ad57fa1c7f1812a19da6a20547')
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
