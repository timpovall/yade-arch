# Maintainer: bunnychow <timpovall@gmail.com>

pkgname=yade
pkgver=1.14.0
pkgrel=1
pkgdesc="Extensible open-source framework for discrete numerical models, focused on Discrete Element Method. The computation parts are written in c++ using flexible object model, allowing independent implementation of new algorithms and interfaces. Python is used for rapid and concise scene construction, simulation control, postprocessing and debugging."
arch=('any')
url='https://yade-dem.org'
license=('GPLv2')
#python-pygraphviz 	-> 	python2-pygraphviz
#python-imaging		->	python2-pillow
depends=('cmake' 'gcc' 'gdb' 'gl2ps' 'freeglut' 'loki-lib' 'boost' 'fakeroot' 'python2' 'ipython2' 'python2-matplotlib'
         'sqlite'
         'python2-numpy' 'tk' 'gnuplot' 'gts' 'pygts' 'python2-pygraphviz' 'vtk' 'eigen3'
         'python2-xlib' 'python2-pyqt4' 'gtk-engines' 'qt4' 'python2-pillow'
         'python2-sphinx' 'libxmu' 'libxi' 'gmp' 'cgal' 'help2man'
         'suitesparse' 'metis' 'openblas')
makedepends=('cmake')
optdepends=('jquery: javascript library for documentation'
            'python-bibtex: parsing bibtex with python for documentation')
provides=('yade' 'yade-batch')
source=("https://github.com/yade/trunk/archive/${pkgver}.tar.gz")
sha1sums=('d6d912e4d935bca7edf59f163e3c5e546fa2fdec')

build() {
	# MAJOR BUG
	# Problem in /usr/include/eigen3/Eigen/src/CholmodSupport/CholmodSupport.h
	# "UF_long" in line 81 must change to "long", the following operation needs root access :-(
    # sudo sed -i 's/UF_long/long/g' /usr/include/eigen3/Eigen/src/CholmodSupport/CholmodSupport.h
	# Temporary fix of a bug:
	# The file trunk-1.14.0/cMake/FindVTK.cmake" does not exist.
	# Here we just comment out the line that calls it
	sed -e '/FindVTK/ s/^#*/#/' -i trunk-${pkgver}/CMakeLists.txt
	
	msg2 "Building..."
	mkdir -p build
	cd build
	cmake ../trunk-${pkgver} \
		-DCMAKE_BUILD_TYPE=Release \
		-DCHUNKSIZE=2 \
		 -DCMAKE_INSTALL_PREFIX=/usr \
		 -DINSTALL_PREFIX=/usr \
		 -DLIBRARY_OUTPUT_PATH=lib \
		-DPYTHON_EXECUTABLE=/usr/bin/python2.7 \
		
		# cmake ../trunk \
		# -DCMAKE_BUILD_TYPE=Release \
		# -DCHUNKSIZE=2 \
		#  -DCMAKE_INSTALL_PREFIX=/usr \
		#  -DINSTALL_PREFIX=/usr \
		#  -DLIBRARY_OUTPUT_PATH=lib \
		# -DPYTHON_EXECUTABLE=/usr/bin/python2.7 \
}

package() {
	cd build
	msg2 "installing to $pkgdir/"
	make DESTDIR="$pkgdir/" install
}