# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=network-minihttp
pkgname=haskell-network-minihttp
pkgver=0.2
pkgrel=4
pkgdesc="A ByteString based library for writing HTTP(S) servers and clients."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:BSD3')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-hsopenssl>=0.4.1' 'haskell-binary>=0.4' 'haskell-binary-strict>=0.3' 'haskell-bytestring=0.9.1.7' 'haskell-containers=0.3.0.0' 'haskell-filepath=1.1.0.4' 'haskell-mtl>=1.1.0.0' 'haskell-network=2.2.1.7' 'haskell-network-bytestring>=0.1.1.2' 'haskell-network-connection>=0.1' 'haskell-network-dns>=0.1.2' 'haskell-old-locale=1.0.0.2' 'haskell-stm=2.1.2.1' 'haskell-tagsoup>=0.5' 'haskell-time=1.1.4' 'haskell-unix=2.4.0.2')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
md5sums=('046bad5270a02b0e1dab9993a778bef5')
