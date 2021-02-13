# Maintainer: Alexandr Parkhomenko <it@52tour.ru>

_author=google-research
_pkgname=ravens
pkgname=${_pkgname}-git
pkgver=1.18
pkgrel=1
pkgdesc='Ravens is a collection of simulated tasks in PyBullet for learning vision-based robotic manipulation, with emphasis on pick and place. It features a Gym-like API with 10 tabletop rearrangement tasks, each with (i) a scripted oracle that provides expert demonstrations (for imitation learning), and (ii) reward functions that provide partial credit (for reinforcement learning).'
arch=(
 'any'
#  'x86_64'
)

url='https://github.com/'
license=('GPL3')
depends=( 
'absl-py>=0.7.0'
'python-gym>0.17.3' #aur
'python-numpy>=1.18.5'
#pybullet>=3.0.4 #!!! pip install
'python-matplotlib>=3.1.1'
'opencv>=4.1.2.30'
'python-meshcat-git>=0.0.18' #aur my
'python-scipy>=1.4.1'
'python-scikit-image>=0.17.2' #aur #arch4edu
'tensorflow-cuda>=2.3'
'python-tensorflow-addons-cuda-git'  #aur  >=0.11.2  latest
#tensorflow_hub==0.9.0
'python-transforms3d=0.3.1' #aur
)
makedepends=('git')
source=("git://github.com/$_author/$_pkgname")
sha256sums=('SKIP')

prepare() {
  cd "$srcdir/$_pkgname"
  git submodule init
  git submodule update
  git fetch --tags
}

pkgver () {
  cd "$srcdir/$_pkgname"
#  git describe --tags --long | sed -r 's/^v//;s/-RC/RC/;s/([^-]*-g)/r\1/;s/-/./g'
  git rev-list --count HEAD  | sed -r 's/^/1./'
}

build() {
  cd "$srcdir/$_pkgname"
  python setup.py build
}

check() {
  cd "$srcdir/$_pkgname"
#  python setup.py test  # No matching distribution found for tensorflow>=2.3.0
}

package() {
  cd "$srcdir/$_pkgname"
  python setup.py install --root="$pkgdir/" --skip-build --optimize=1
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
