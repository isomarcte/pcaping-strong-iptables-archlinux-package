# Maintainer: David Strawn <isomarcte@gmail.com>
pkgname=pcaping-strong-iptables
pkgver=2.1.0
pkgrel=1
pkgdesc='A packet capturing iptables based firewall.'
url="https://github.com/isomarcte/${pkgname}"
license=('BSD')
source=("https://github.com/isomarcte/${pkgname}/archive/${pkgver}.tar.gz")
md5sums=('0f30c11c7fffa04af26ddd3cd72cad5c')
sha1sums=('3457279f288617ed4c7324e7a234ae7a3dd93a0b')
sha256sums=('62b038ba31e18b0f402122aaae79b3093c64035c40efd39c9de2323e54c96ca9')
sha384sums=('438ca7c855ee184aac899f1ac4b8bbd02029fee8fe4f0eb1c309fbf5a5bda46fe5482d6c1c2af5d0ae1434f125a6f4c9')
sha512sums=('da395bbc5ff960f6b54e3b5568d198fc3a465d75b7a62e5ab26777294b1b82d92df5c2f7d8a0872e44faa803edb8f7e2d8384144c7995df822dc5e4e5da9addd')
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
