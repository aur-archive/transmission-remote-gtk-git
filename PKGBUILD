# Maintainer: swanson <webaake@gmail.com>
# Contributor: Aleksey Frolov <atommixz@gmail.com> [ru]
# Contributor: PitBall

_pname=transmission-remote-gtk
pkgname=${_pname}-git
pkgver=20140122
pkgrel=1
pkgdesc="GTK client for remote management of the Transmission BitTorrent client, using its HTTP RPC protocol"
arch=(i686 x86_64)
license=('GPL2')
depends=('git' 'gtk3' 'hicolor-icon-theme' 'geoip' 'libproxy' 'json-glib' 'libnotify' 'desktop-file-utils' 'curl')
makedepends=('intltool')
conflicts=('transmission-remote-gtk')
install=${pkgname}.install
options=('!libtool')
url="http://code.google.com/p/transmission-remote-gtk"

_gittrunk="https://code.google.com/p/transmission-remote-gtk/"
_gitmod=${pkgname}

build() {
	cd ${srcdir}

# GIT checkout
	if [[ -d ${_gitmod} ]]; then
		(cd ${_gitmod} && git pull )
	else
		git clone ${_gittrunk} ${_gitmod}
	fi

	rm -rf ${srcdir}/${_gitmod}-build
	cp -r ${srcdir}/${_gitmod} ${srcdir}/${_gitmod}-build
	cd ${srcdir}/${_gitmod}-build

# Configure
	./autogen.sh
	./configure \
	--prefix=/usr

# Compile
	make
}

package() {
	cd ${srcdir}/${_gitmod}-build
# Install
	make DESTDIR=${pkgdir} install

# License & Authors
	install -dm755 ${pkgdir}/usr/share/licenses/${_pname}
	ln -sf /usr/share/licenses/common/GPL2/license.txt ${pkgdir}/usr/share/licenses/${_pname}/LICENSE
	install -Dm644 AUTHORS ${pkgdir}/usr/share/doc/${_pname}/AUTHORS
}
