# Maintainer: Aaron Ali <t0nedef@causal.ca>
# Contributor: Richard Kakaš <richard.kakas@gmail.com>

pkgname="brscan2-network"
pkgver="0.2.5"
pkgrel="8"
license=('GPL')
url="http://welcome.solutions.brother.com/bsc/public_s/id/linux/en/download_scn.html#brscan2"
pkgdesc="SANE drivers from Brother for scanners on a network"

arch=('i686' 'x86_64')
depends=('sane')
makedepends=('rpmextract')
provides=('brscan2')
conflicts=('brscan2')

_arch="i386"
if [ "$CARCH" == "x86_64" ]; then 
	_arch="x86_64"
fi

install=brscan2-network.install
source=(http://www.brother.com/pub/bsc/linux/dlf/brscan2-$pkgver-1.$_arch.rpm)

md5sums=('944432983dcb918704862147b2a27977')
if [ "$CARCH" == "x86_64" ]; then 
	md5sums=('88ab217b814ba87ac855b21dc037e0ac')
fi

build() {
	cd $srcdir
	for i in *.rpm; do
		rpmextract.sh "$i"
	done
}

package() {
	mkdir -p $pkgdir/usr/bin
	cp -R $srcdir/usr/bin/* $pkgdir/usr/bin/
	cp -R $srcdir/usr/local/ $pkgdir/usr/
	# handle libs
	if [ "$CARCH" == "x86_64" ]; then 
		cp -R $srcdir/usr/lib64/ $pkgdir/usr/lib
		cd $pkgdir/usr/lib
		for lib in `ls * sane/*`; do
			if [ -L $lib ]; then
				ln=`ls -al $lib | awk '{print $NF}' | sed 's|lib64|lib|'`
				rm $lib
				ln -s $ln $lib
			fi
		done
	else
		cp -R $srcdir/usr/lib/ $pkgdir/usr/
	fi
}

