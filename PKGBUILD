pkgname=strigi-git
pkgver=v0.7.8.2.g0b7eb7d
pkgrel=1
pkgdesc='Fast crawling desktop search engine'
arch=('i686' 'x86_64')
url='http://www.kde.org'
license=('LGPL')
depends=('exiv2' 'libxml2' 'boost-libs')
makedepends=('git' 'cmake' 'boost')
conflicts=('kf5-strigi')
provides=('kf5-strigi')
source=(git://anongit.kde.org/strigi.git
        git://anongit.kde.org/libstreams.git
        git://anongit.kde.org/libstreamanalyzer.git
        git://anongit.kde.org/strigiutils.git
        git://anongit.kde.org/strigidaemon.git
        git://anongit.kde.org/strigiclient.git)
md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

pkgver() {
  cd strigi
  git describe --always | sed 's|-|.|g'
}

prepare() {
  cd strigi
  git submodule init
  git config submodule.libstreams.url "${srcdir}"/libstreams
  git config submodule.libstreamanalyzer.url "${srcdir}"/libstreamanalyzer
  git config submodule.strigiutils.url "${srcdir}"/strigiutils
  git config submodule.strigidaemon.url "${srcdir}"/strigidaemon
  git config submodule.strigiclient.url "${srcdir}"/strigiclient
  git submodule update
}

build() {
  mkdir -p build
  cd build
  cmake ../strigi \
    -DCMAKE_BUILD_TYPE=Release \
	-DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_SKIP_RPATH=ON \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DENABLE_INOTIFY=ON \
    -DENABLE_LOG4CXX=OFF \
    -DENABLE_FAM=OFF \
    -DENABLE_CLUCENE=OFF \
    -DENABLE_CLUCENE_NG=OFF \
    -DENABLE_FFMPEG=OFF \
    -DENABLE_QT4=OFF
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
}
