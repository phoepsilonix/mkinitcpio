# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Dave Reisner <dreisner@archlinux.org>
# Maintainer: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=30
pkgrel=3
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url="https://projects.archlinux.org/mkinitcpio.git/"
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive' 'coreutils'
         'bash' 'diffutils' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'systemd')
optdepends=('xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'zstd: Use zstd compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
provides=('initramfs')
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.gz"{,.sig}
        manjaro.patch ab6bad7.patch add-vmd-module-with-block.patch)
install=mkinitcpio.install
sha256sums=('c7725035a06d2ab6ef6e97601b69859d6061aec95c4551e2a1ad2e27d307258f'
            'SKIP'
            'f6a619c2dfc5a6bdd4596d9b4d9f7fdcce3ee0244390161cab51ef646b7317f8'
            'b90b5d74a1591840e727572dca0ec7ae7c36ed19dedc02a393802ed2aad23ce4'
            '2236841bb5d16ce01760aba480c1a5ac43c0d9841cc617c499d107e17f0159d7')
validpgpkeys=('ECCAC84C1BA08A6CC8E63FBBF22FB1D78A77AEAB'    # Giancarlo Razzolini
              '86CFFCA918CF3AF47147588051E8B148A9999C34')   # Evangelos Foutras

prepare() {
  cd "$pkgname-$pkgver"
  # Add changes of Manjaro
  patch -p1 -i ../manjaro.patch
  patch -p1 -i ../add-vmd-module-with-block.patch
  patch -Rp1 -i ../ab6bad7.patch
}

check() {
  make -C "$pkgname-$pkgver" check
}

package() {
  make -C "$pkgname-$pkgver" DESTDIR="$pkgdir" install

  # https://www.archlinux.org/todo/alpm-hooks-should-use-type-path-not-file/
  sed -i -e 's|File|Path|' "$pkgdir"/usr/share/libalpm/hooks/*hook
}
