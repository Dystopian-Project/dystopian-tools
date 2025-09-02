# Maintainer: DCx7C5 <dcxdevelopment@protonmail.com>
# Contributor: DCx7C5 <dcxdevelopment@protonmail.com>
# Project: Dystopian Project

pkgbase=dystopian-tools
pkgver=0.1.0
pkgrel=1
pkgdesc="A meta package for dystopian-themed tools"
arch=('any')
url="https://github.com/Dystopian-Project/dystopian-tools"
license=('MIT')
makedepends=(
    'git'
    'gnupg'
    'systemd'
    'efitools'
)

depends=('wget' 'curl')
provides=('dystopian-tools')
conflicts=('dystopian-tools')
install="${pkgbase}.install"

_srcname=${pkgbase}-${pkgver%.*}
_srctag=v${pkgver%.*}-${pkgver##*.}

# Sources (fill as needed)
source=(
    "$pkgbase-"
)
sha256sums=(

)
b2sums=(

)

#
# Top-level package
#

_package() {
    install -d "${pkgdir}/usr/share/doc/dystopian-tools" \
               "${pkgdir}/usr/lib/dystopian-tools" \
               "${pkgdir}/usr/bin"

    install -m 644 README.md "${pkgdir}/usr/share/doc/dystopian-tools/README.md"
    install -m 640 lib/variables.sh "${pkgdir}/usr/lib/dystopian-tools/variables.sh"
    install -m 640 lib/helper.sh "${pkgdir}/usr/lib/dystopian-tools/helper.sh"
}

#
# Subpackage implementations
#
_package-crypto() {
    pkgdesc="Cryptographic helper tools for certificate and key management"
    depends=(
        "dystopian-tools"
        "openssl"
        "gnupg"
    )
    provides=('dystopian-crypto')
    conflicts=('dystopian-crypto')
    install="${pkgbase}.install"

    install -d "${pkgdir}/usr/bin" \
               "${pkgdir}/usr/lib/dystopian-tools"

    install -m 750 bin/dystopian-crypto "${pkgdir}/usr/bin/dystopian-crypto"
    install -m 640 lib/crypto-db.sh "${pkgdir}/usr/lib/dystopian-tools/crypto-db.sh"
    install -m 640 lib/ssl.sh "${pkgdir}/usr/lib/dystopian-tools/ssl.sh"
    install -m 640 lib/gpg.sh "${pkgdir}/usr/lib/dystopian-tools/gpg.sh"

    install -d -m 755 "${pkgdir}/etc/dystopian-crypto"
    install -d -m 755 "${pkgdir}/etc/dystopian-crypto/ca"
    install -d -m 750 "${pkgdir}/etc/dystopian-crypto/ca/private"
    install -d -m 755 "${pkgdir}/etc/dystopian-crypto/cert"
    install -d -m 750 "${pkgdir}/etc/dystopian-crypto/cert/private"
    install -d -m 750 "${pkgdir}/etc/dystopian-crypto/old"
    install -d -m 700 "${pkgdir}/etc/dystopian-crypto/gnupg"
    install -d -m 755 "${pkgdir}/etc/dystopian-crypto/crl"

    install -m 600 conf/crypto-db.json "${pkgdir}/etc/dystopian-crypto/crypto-db.json"
}

_package-secboot() {
    pkgdesc="Secure Boot utilities and enrollment helpers"
    depends=('dystopian-tools' 'dystopian-crypto' 'efitools' 'systemd')
    provides=('dystopian-secboot')
    conflicts=('dystopian-secboot')
    install="${pkgbase}.install"

    install -d "${pkgdir}/usr/bin" "${pkgdir}/usr/lib/dystopian-tools"

    install -m 750 bin/dystopian-secboot "${pkgdir}/usr/bin/dystopian-secboot"

    install -m 640 lib/secboot.sh "${pkgdir}/usr/lib/dystopian-tools/secboot.sh"
    install -m 640 lib/secboot-db.sh "${pkgdir}/usr/lib/dystopian-tools/secboot-db.sh"

    install -d -m 700 "${pkgdir}/etc/dystopian-secboot"
    install -d -m 700 "${pkgdir}/etc/dystopian-secboot/ms"

    install -m 600 conf/secboot-db.json "${pkgdir}/etc/dystopian-secboot/secboot-db.json"
}

# Split packages (actual package names)
pkgname=(
  "$pkgbase"
  "$pkgbase-crypto"
  "$pkgbase-secboot"
)

for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done


# vim:set ts=8 sts=2 sw=2 et:
