# Maintainer: Anatol Pomozov
# Maintainer: Filipe Lains (FFY00) <lains@archlinux.org>
# Contributor: Thomas Krug <t.krug@elektronenpumpe.de>

pkgname=libsigrokdecode
pkgver=0.5.3
pkgrel=7
pkgdesc='C library that provides protocol decoding for logic analyzers, protocol decoders, etc.'
arch=('x86_64')
url='https://www.sigrok.org/wiki/Libsigrokdecode'
license=('GPL3')
depends=('glib2' 'python')
	#"git@github.com:AtomicFS/libsigrokdecode.git"
source=(
	"git+https://github.com/AtomicFS/libsigrokdecode.git"
        $pkgname-py39.patch::https://github.com/sigrokproject/libsigrokdecode/commit/9b0ad5177bd6.patch
        use-python3-embed.pc-as-a-fallback.patch)
sha512sums=('SKIP'
            'f1b26c227fc0eb5e831563e328a20beeb2412576bc50a0a241923dad1ebd1bd0eb07f2b3a4230ba99e3bf8db04cac6480ed8724e9727514d65cb3afe6838e189'
            'a4b22157898308cd248decf977e637e214c8f75aca2b8af4803a01208d0cbbe11ddb232e3d356e531e72c43a1a0ff07bc08e30f8378fa67f23f23665a7e53cb1')

prepare() {
  cd ${pkgname}
  patch -Np1 -i ../${pkgname}-py39.patch
  # https://sourceforge.net/p/sigrok/mailman/message/37168276/
  patch -Np1 -i ../use-python3-embed.pc-as-a-fallback.patch
}

build() {
  cd ${pkgname}

  autoreconf --force --install . # it is a content of upstream's ./autogen.sh
  ./configure --prefix=/usr

  make
}

package() {
  cd ${pkgname}

  make DESTDIR="${pkgdir}" install
}

