# Maintainer: Philip Müller <philm@manjaro.org>
# Arch Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Arch Maintainer: Dave Reisner <dreisner@archlinux.org>
# Arch Maintainer: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=27
pkgrel=1.2
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url="https://projects.archlinux.org/mkinitcpio.git/"
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive'
         'coreutils' 'bash' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'systemd')
optdepends=('xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
provides=('initramfs')
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.gz"{,.sig}
        manjaro.patch)
install=mkinitcpio.install
sha256sums=('e6bff1cb78b677538eb9aace900b715fd59de8fc210b74fb9d899dfaa32bc354'
            'SKIP'
            'f6a619c2dfc5a6bdd4596d9b4d9f7fdcce3ee0244390161cab51ef646b7317f8')
validpgpkeys=('487EACC08557AD082088DABA1EB2638FF56C0C53'   # Dave Reisner
              '86CFFCA918CF3AF47147588051E8B148A9999C34'   # Evangelos Foutras
              'ECCAC84C1BA08A6CC8E63FBBF22FB1D78A77AEAB')  # Giancarlo Razzolini

check() {
  make -C "$pkgname-$pkgver" check
}

prepare() {
  cd "$pkgname-$pkgver"
  patch -p1 -i ../manjaro.patch
  cd ..
}

package() {
  make -C "$pkgname-$pkgver" DESTDIR="$pkgdir" install
}
