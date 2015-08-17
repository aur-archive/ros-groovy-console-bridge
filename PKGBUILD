pkgdesc="ROS - Lightweight tool for forwarding output from libraries to other logging systems."
url='http://www.ros.org/'

pkgname='ros-groovy-console-bridge'
pkgver='0.2.4'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-catkin
  boost)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/console_bridge ]; then
    cd ${srcdir}/console_bridge
    git fetch origin --tags
    git reset --hard release/groovy/console_bridge/${pkgver}-0
  else
    git clone -b release/groovy/console_bridge/${pkgver}-0 git://github.com/ros-gbp/console_bridge-release.git ${srcdir}/console_bridge
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/console_bridge
  cmake ${srcdir}/console_bridge -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
