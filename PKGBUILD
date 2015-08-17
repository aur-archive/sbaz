# $Id: PKGBUILD 78820 2012-10-25 06:47:28Z foutrelis $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>

pkgname=sbaz
pkgver=2.1
pkgrel=2
pkgdesc="Bazaar software package manager for Scala"
arch=('any')
url="http://www.lexspoon.org/sbaz/"
license=('GPL')
depends=('java-runtime=6' 'scala' 'sh')
makedepends=('apache-ant' 'tomcat7' 'openjdk6' 'texlive-bin')
# See http://lampsvn.epfl.ch/svn-repos/scala/sbaz/tags/ for snapshots
source=(http://archlinux-stuff.googlecode.com/files/sbaz-20110602.svn.tar.gz
	sbaz.sh.patch)
md5sums=('ce19951ac3fe14382904a7a1db522397'
         '48365f2ee7b958f1c663f097f03f60dc')

build(){
    cd ${srcdir}/${pkgname}.svn

    cat >build.properties <<EOF
java6-rt.jar=/usr/lib/jvm/java-6-openjdk/jre/lib/rt.jar
scala.home=/usr/share/scala
EOF

    ant downloadDeps
    ant dist
}

package() {
    cd ${srcdir}/${pkgname}.svn

    mkdir -p $pkgdir/usr/share/scala
    cd $pkgdir/usr/share/scala
    jar xf $srcdir/sbaz.svn/dists/sbaz-$pkgver.sbp

    rm -f bin/sbaz.bat
    chmod 0755 bin/sbaz
    patch -p0 bin/sbaz <$srcdir/sbaz.sh.patch
    install -D -m0755 bin/sbaz $pkgdir/usr/bin/sbaz
}
