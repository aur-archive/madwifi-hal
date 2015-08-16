# Contributor: Kravchuk Sergei <alfss.obsd@gmail.com>

_kernver=`uname -r`
pkgname=madwifi-hal
pkgver=0.10.5.6r4126
pkgrel=1
_rpkgver=0.10.5.6-r4126-20100324
pkgdesc="Madwifi hal branch drivers for Atheros wireless chipsets. For stock arch 2.6 kernel"
arch=('i686' 'x86_64')
license=('GPL')
url="http://madwifi-project.org/"
depends=('kernel26 kernel26-headers')
install=${pkgname}.install
source=(http://snapshots.madwifi-project.org/${pkgname}-0.10.5.6/${pkgname}-${_rpkgver}.tar.gz)
md5sums=('583f60b7885700bc3dcf779dbb328798')

build() {
	cd ${srcdir}/${pkgname}-${_rpkgver}
	sed -i -e 's/-Werror//g' Makefile.inc
	make KERNELPATH=/lib/modules/$_kernver/build KERNELRELEASE=$_kernver all || return 1
	make DESTDIR=${pkgdir} \
	BINDIR=/usr/bin \
	MANDIR=/usr/share/man install || return 1
	sed -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${_kernver}'/" $startdir/*.install

	# install to wireless kernel directory
	mkdir -p $pkgdir/lib/modules/$_kernver/kernel/drivers/net/wireless/madwifi
	mv $pkgdir/lib/modules/$_kernver/net/* $pkgdir/lib/modules/$_kernver/kernel/drivers/net/wireless/madwifi
	rm -r $pkgdir/lib/modules/$_kernver/net/
}
