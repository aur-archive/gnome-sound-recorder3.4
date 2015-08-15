# $Id: PKGBUILD 101758 2013-11-30 18:46:32Z bgyorgy $
# Maintainer: Balló György <ballogyor+arch at gmail dot com>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=gnome-sound-recorder3.4
_pkgname=gnome-media
pkgver=3.4.0
pkgrel=1
pkgdesc="Legacy sound recorder for GNOME (part of gnome-media)"
arch=('i686' 'x86_64')
license=('GPL')
depends=('libgnome-media-profiles' 'gstreamer0.10-good-plugins')
makedepends=('intltool' 'gnome-doc-utils')
optdepends=('gstreamer0.10-ugly-plugins: Record sound into mp3 format')
conflicts=('gnome-sound-recorder' 'gnome-media')
url="https://git.gnome.org/browse/gnome-media"
install=$pkgname.install
source=(http://ftp.gnome.org/pub/gnome/sources/$_pkgname/${pkgver:0:3}/$_pkgname-$pkgver.tar.xz
        grecord-add-PULSEPROPmediarole.patch
        grecord-Should-call-gnome-control-center-sound-not.patch
        grecord-send-eos-before-we-stop-record.patch)
sha256sums=('a76fac286f24d3836137ddbaab66f05e19eb5fb83cca6e375dbef040765a1d1f'
            '7abd86638ccde30232455ea66a7aff244f5c1cc5f3620b85f0215bf4bd07d546'
            '6c8af4bf741d702ce3722cc2bfd1b7caa44f142776706157851184fb2bc55e04'
            '5feb1e447f9ac575b282b05be9bfc946794635f98f63cf24603f931767ec8f9d')

prepare() {
  cd "$_pkgname-$pkgver"

  # Avoid conflict with other components of gnome-media
  sed -i 's/GETTEXT_PACKAGE=gnome-media-2.0/GETTEXT_PACKAGE=gnome-sound-recorder/' configure

  # Upstream fixes
  patch -Np1 -i "$srcdir/grecord-add-PULSEPROPmediarole.patch"
  patch -Np1 -i "$srcdir/grecord-Should-call-gnome-control-center-sound-not.patch"
  patch -Np1 -i "$srcdir/grecord-send-eos-before-we-stop-record.patch"
}

build() {
  cd "$_pkgname-$pkgver"
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
              --disable-schemas-install --disable-gstprops \
              --with-gconf-schema-file-dir=/usr/share/gconf/schemas
  make
}

package() {
  cd "$_pkgname-$pkgver"
  make DESTDIR="$pkgdir" install
}
