pkgname=ksh93
pkgver=93u
pkgrel=1
pkgdesc="The Original AT&T Korn Shell"
arch=('x86_64')
url="http://kornshell.org/"
license=('EPL')
provides=('ksh' 'ksh94')
conflicts=('ksh' 'ksh93')
install=ksh93.install
source=("${pkgname}::git+https://github.com/att/ast.git#branch=2012-08-01-master")
md5sums=('SKIP')

build() {
    cd "${srcdir}/${pkgname}"
    bin/package make
}

package() {

    cd "${srcdir}/${pkgname}"
    _arch=$(bin/package host)

    install -dm 755 "${pkgdir}/usr/share/${pkgname}" 

    install -Dm 755 "arch/${_arch}/bin/ksh" "${pkgdir}/usr/bin/ksh"

    ln -sf "rksh" "${pkgdir}/usr/bin/rksh"
    ln -sf "pfksh" "${pkgdir}/usr/bin/pfksh"

    install -Dm 644 "src/cmd/ksh93/sh.1" "${pkgdir}/usr/share/man/man1/ksh.1"

    ln -sf "ksh.1" "${pkgdir}/usr/share/man/man1/rksh.1"
    ln -sf "ksh.1" "${pkgdir}/usr/share/man/man1/pfksh.1"

    install -dm 755 "${pkgdir}/usr/share/${pkgname}/functions" 

    local _fun
    for _fun in dirs popd pushd title ; do
        install -Dm 644 "arch/${_arch}/fun/${_fun}" "${pkgdir}/usr/share/${pkgname}/functions"
    done

    install -dm 755 "${pkgdir}/usr/share/doc/${pkgname}" 

    local _doc
    for _doc in COMPATIBILITY DESIGN OBSOLETE README RELEASE RELEASE88 RELEASE93 TYPES sh.memo builtins.mm ; do
        install -Dm 644 "src/cmd/ksh93/${_doc}" "${pkgdir}/usr/share/doc/${pkgname}/${_doc}"
    done

}

