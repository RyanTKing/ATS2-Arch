# Maintainer: Ryan King <hello@ryanking.com>

pkgname=ats2
pkgver=0.2.12
pkgdesc="Major Release 2 of the ATS2 Programming Language"
arch=('i686' 'x86_64')
url="http://www.ats-lang.org"
license=('MIT')
depends=('gcc' 'glibc' 'gmp' 'json-c' 'python' 'clojure')
makedepends=('git')
install="$pkgname.install"
source=('main::git://git.code.sf.net/p/ats2-lang/code'
        'contrib::git://github.com/githwxi/ATS-Postiats-contrib.git')
pkgrel=1
sha1sums=('SKIP' 'SKIP')

build() {
    # Setup variables
    export PATSHOME="$srcdir/main"
    export PATSHOMERELOC="$srcdir/contrib"
    export PATH="$PATSHOME/bin:$PATH"

    # Build patsopt/patscc
    cd "$PATSHOME"
    ./configure
    make all

    # Z3 Solver
    cd "$PATSHOMERELOC/projects/MEDIUM/ATS-extsolve"
    # make DATS_C
    cd "ATS-extsolve-z3"
    make build
    mv patsolve_z3 "$PATSHOME/bin/patsolve_z3"

    # For parsing C code
    cd "$PATSHOMERELOC/projects/MEDIUM/CATS-parsemit"
    make DATS_C

    # For compiling into Javascript
    cd "$PATSHOMERELOC/projects/MEDIUM/CATS-atsccomp/CATS-atscc2js"
    make build
    mv atscc2js "$PATSHOME/bin/atscc2js"

    # Compile to Python 3
    cd "$PATSHOMERELOC/projects/MEDIUM/CATS-atsccomp/CATS-atscc2py3"
    make build
    mv atscc2py3 "$PATSHOME/bin/atscc2py3"

    # Compile to Clojure
    cd "$PATSHOMERELOC/projects/MEDIUM/CATS-atsccomp/CATS-atscc2clj"
    make build
    mv atscc2clj "$PATSHOME/bin/atscc2clj"
}

package() {
    # Move everything to share
    cd $srcdir
    sudo rm -rf /usr/share/ATS2
    sudo mkdir -p /usr/share/ATS2
    sudo cp -r main /usr/share/ATS2/main
    sudo cp -r contrib /usr/share/ATS2/contrib
}
