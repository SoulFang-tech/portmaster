# Maintainer: Vedanta Singh <vedant0102@outlook.com>
# Contributor:  Patrick Pacher <patrick@safing.io>
pkgname=portmaster
pkgver=0.5.2
pkgrel=1
pkgdesc='Application Firewall: Block Mass Surveillance - Love Freedom'
arch=('x86_64')
license=('AGPL3')
install=arch.install
depends=('libnetfilter_queue' 'webkit2gtk')
makedepends=('imagemagick') # for convert
optdepends=('libappindicator-gtk3: for systray indicator')
options=('!strip')
#changelog=
source=("portmaster-start::https://updates.safing.io/linux_amd64/start/portmaster-start_v${pkgver//./-}"
		'./portmaster.desktop'
		'./portmaster_notifier.desktop'
		'./portmaster_logo.png'
		'./portmaster.service')
noextract=('portmaster-start')
md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

prepare() {
	for res in 16 32 48 96 128 ; do
		local iconpath=${pkgname}-${pkgver}/icons/${res}x${res}/apps
		mkdir -p ${iconpath} ; 
		convert ./portmaster_logo.png -resize ${res}x${res} ${iconpath}/portmaster.png ; 
	done
}

build() {
	mkdir -p ${pkgname}-${pkgver}/data
	chmod a+x ${srcdir}/portmaster-start
	${srcdir}/portmaster-start --data ${pkgname}-${pkgver}/data update
}

package() {
	mkdir -p ${pkgdir}/var/lib/portmaster
	mkdir -p ${pkgdir}/usr/lib/systemd/system
	mkdir -p ${pkgdir}/usr/share/icons/hicolor/
	mkdir -p ${pkgdir}/usr/share/applications/
	cp ${srcdir}/portmaster.service ${pkgdir}/usr/lib/systemd/system/portmaster.service
	cp ${srcdir}/portmaster-start ${pkgdir}/var/lib/portmaster/
	cp -r ${srcdir}/${pkgname}-${pkgver}/data/* ${pkgdir}/var/lib/portmaster/
	cp -r ${srcdir}/${pkgname}-${pkgver}/icons/* ${pkgdir}/usr/share/icons/hicolor/
	cp ${srcdir}/portmaster.desktop ${pkgdir}/usr/share/applications/
	cp ${srcdir}/portmaster_notifier.desktop ${pkgdir}/usr/share/applications/
}
