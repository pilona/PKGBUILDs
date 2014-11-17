# Maintainer: Andreas B. Wagner <AndreasBWagner@pointfree.net>
# Maintainer: Bhoppi Chaw <bhoppi@hotmail.com>
# Contributor: Thiago Coutinho
# Contributor: Thomas Dziedzic
# Contributor: Alex Pilon

pkgname=ns-3
pkgver=3.21
pkgrel=1
pkgdesc='Discrete-event network simulator to replace ns-2'
arch=('i686' 'x86_64')
url='http://www.nsnam.org/'
license=('GPL')
#makedepends=('imagemagick' 'openmpi')
depends=('gsl' 'gtk2' 'libxml2' 'python2' 'sqlite3')
optdepends=('python2-pygraphviz' 'pygoocanvas')
#optdepends=('openmpi: mpi support')
source=("https://www.nsnam.org/release/ns-allinone-$pkgver.tar.bz2")
md5sums=('b099fe267275bfd3806b08a7e386142f')

prepare() {
	cd $srcdir/ns-allinone-$pkgver/
	# Fix the shebang line in some scripts.
	find -type f -name '*.py' -exec sed -i '1s/python/python2/g' {} +
	# Work around hardcoded qmake path in /usr/local prefix.
	grep -rl '/usr/local' . | xargs sed -i 's#/usr/local#/usr#g'
}

build() {
	cd $srcdir/ns-allinone-$pkgver/
	./build.py \
		--enable-examples \
		--enable-tests \
		-- \
		--prefix=/usr \
		--with-python=python2 \
        --build-profile=release
}

check() {
	cd $srcdir/ns-allinone-$pkgver/ns-$pkgver
	python2 ./waf check
}

package() {
	cd $srcdir/ns-allinone-$pkgver/ns-$pkgver
	python2 ./waf --destdir=$pkgdir/ --build-profile=release install
}
