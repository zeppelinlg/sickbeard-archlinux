# Maintainer: sudokode <sudokode@gmail.com>
# Previous Maintainer: Crass00 <crass00 at hotmail dot com>
# Previous Maintainer: Superstar655 <choman000 at hotmail dot com>
# Contributor: Augusto Born de Oliveira <augustoborn at gmail dot com>

pkgname=sickbeard-git
pkgver=3756.d4d3698
pkgrel=2
pkgdesc="A PVR application that downloads and manages your TV shows"
arch=('any')
url="http://code.google.com/p/sickbeard/"
license=('GPL3')
depends=('python2' 'python2-cheetah')
makedepends=('git')
optdepends=('sabnzbd: NZB downloader'
            'python2-notify: desktop notifications')
install=sickbeard.install
conflicts=('sickbeard')
backup=('etc/sickbeard.conf')
source=("$pkgname::git://github.com/midgetspy/Sick-Beard.git"
        'sickbeard-system.service' 'sickbeard-user.service' 'sickbeard.tmpfile')
sha256sums=('SKIP'
            'f902cdd7c12dab874067238ccd536795614f918273943f73678bd1dbf9b57cb8'
            'a52ed1f41af332015084a8da6fcf08ec2437d25535ed5f4160e42788673cbe90'
            'af80fd7ad2adb0e4173f922d50f0560feb1548f0e589fee6691a69b19fc2499e')

pkgver() {
  cd $pkgname

  echo "$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {
  cd $pkgname

  # Fix python2 shebang
  sed -i 's/python/python2/g' autoProcessTV/sabToSickBeard.py
  sed -i 's/python/python2/g' autoProcessTV/hellaToSickBeard.py
}

package() {
  mkdir -p "$pkgdir"/usr/share/sickbeard
  chmod 755 "$pkgdir"/usr/share/sickbeard
  mkdir -p "$pkgdir"/var/lib/sickbeard
  chmod 755 "$pkgdir"/var/lib/sickbeard
  cp -r $pkgname/* "$pkgdir"/usr/share/sickbeard

  mkdir $pkgdir/etc
  touch $pkgdir/etc/sickbeard.conf

  install -D -m644 sickbeard-system.service "$pkgdir"/usr/lib/systemd/system/sickbeard.service
  install -D -m644 sickbeard-user.service "$pkgdir"/usr/lib/systemd/user/sickbeard.service
  install -D -m644 sickbeard.tmpfile "$pkgdir"/usr/lib/tmpfiles.d/sickbeard.conf

  find "$pkgdir" -type d -name '.git' -exec rm -r '{}' +
}

# vim:set ts=2 sw=2 et:
