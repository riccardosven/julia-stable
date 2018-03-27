pkgname=julia-stable
pkgver=0.6.2
pkgrel=1
pkgdesc='The Julia Language: A fresh approach to technical computing.'
arch=('x86_64')
url='https://julialang.org/'
license=('MIT')

source=("${pkgname}-${pkgver}::git+https://github.com/JuliaLang/Julia"
        "Make.user")
sha256sums=('SKIP'
            'b6e9c49e1b9e9529a81b2cb48feff34770351cd79abab2393eb16c29fca9f213')

options=('!strip' 'staticlibs')

makedepends=('libatomic_ops' 'python' 'git' 'cmake>=3.4.3')
depends=('openlibm>=0.5.5' 'openblas-lapack>=0.2.20' 'suitesparse>=4.1'
         'arpack>=3.5.0' 'libgit2>=0.23' 'pcre2>=10.00' 'gmp>=5.0' 'mpfr>=3.0'
         'curl>=7.50' 'libssh2>=1.7' 'mbedtls>=2.2')

provides=('julia')
conflicts=('julia')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  git checkout -b install v${pkgver}
  cp ${srcdir}/Make.user .
  make prefix=/usr --jobs `nproc`
}

check() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make test
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR=${pkgdir} prefix=/usr install
  mv ${pkgdir}/usr/etc ${pkgdir}/etc
}
