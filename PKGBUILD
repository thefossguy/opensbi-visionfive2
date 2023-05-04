# Maintainer: Pratham Patel <thefirst1322@gmail.com>
pkgname=opensbi-visionfive2
pkgver="v1.2+$(date +%Y.%m.%d)"
pkgrel=1
pkgdesc='OpenSBI, for the StarFive VisionFive 2 SBC'
arch=('riscv64')
url='https://github.com/riscv-software-src/opensbi'
license=('BSD-2-Clause')
groups=('firmware-visionfive2')
makedepends=('dtc' 'gcc' 'python')
conflicts=('opensbi')
options=('!lto')
#source=("$pkgname::git+https://github.com/riscv-software-src/opensbi#tag=${pkgver//+/-}")
#sha512sums=('SKIP')

export PLATFORM=generic
export FW_TEXT_START=0x40000000
export FW_OPTIONS=0
export INSTALL_LIB_PATH=lib

prepare() {
    # TODO: remove the manual git clone after a new version of OpenSBI releases
    [[ -d $pkgname ]] || git clone --depth 1 --branch master \
        https://github.com/riscv-software-src/opensbi.git $pkgname
    cd $pkgname
    
    echo "Cleaning any possible build residue..."
    make clean

    # TODO: remove this after a new version of OpenSBI releases
    echo "Pulling in new changes..."
    git pull
}

build() {
    cd $pkgname
    make -j$(nproc)
}

package() {
    cd $pkgname
    make I="$pkgdir/usr" install
}
