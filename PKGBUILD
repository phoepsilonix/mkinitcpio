# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=39
pkgrel=4
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio'
license=('GPL-2.0-only')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive' 'coreutils'
         'bash' 'binutils' 'diffutils' 'findutils' 'grep' 'filesystem>=2011.10-1' 'zstd' 'systemd')
makedepends=('asciidoc')
checkdepends=('bats' 'bats-assert' 'lzop')
optdepends=('gzip: Use gzip compression for the initramfs image'
            'xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
provides=('initramfs')
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.xz"{,.sig}
        # Manjaro patches
        'manjaro.patch'
        'manjaro-extramodules.patch'
        'manjaro-unsupported-modules_from_symbol.patch'
        )
install=mkinitcpio.install
sha512sums=('50ae08ddf7596b821c89f927ff6692ca907a5045590096155ec6de64e0b5da647ff2c75d1603ab0035046096d37a6eacae383d458b1bb36bd525691b2b23c9ea'
            'SKIP'
            '94bfd4d7cf4797f5963aad1e449ee558bc13ac2c5a67326e87aa06df98562fdb4c43a1387dfebc011942bbeaed501df4f9c38898b631e356858b1b7a7351d01d'
            '04f87d5aa3d159045cf25773f3113f9a875d20234ba736f429cdca3ca4f0cb08ee737792ae72ff7a00ac6573fe904cc030cc9adf0a6c5c8e319f370a33872317'
            '6928d41d93dfbb78f3a0f12230a3fb0e039fc1f074de7d147c2930b25316d10ea3dfd516f12b1eaabe8b508a95add3618beb22cf1fdbb374a5b02a0ebd1a4ae8')
b2sums=('3a28d6711ce843aafe2868b09ba5a723e57e4fdffe905ac915aa5d224279590a10bba902933f183de33e08e96a6aad4d9e1d4752be74c011a37c4cbe83c8d645'
        'SKIP'
        '34bd582722588198a7e0c4964e21c992fe3b420b881753eb7403a4aed4fe525b2be5a8ceb2a346be718645ffbd530ea393490b8aa2dbef183c85c5b85bcaf33d'
        '1046085788eea6ee04115d3776a292ae6e336fdc2f99b7a9ff4a6408e6b6a83cc106a41c46ba7fb795f81fcfa48ca1752ea3296f8d701435a49f7cbf107b8c76'
        'e5c9e2f19596b7dc8207ca94d138263edafb1d9dc80bc6177462b109ac66500a64fd72c43657824f65204666c3bf1476d7aa5e8d7f0b9477f176739830c99c6a')
validpgpkeys=('ECCAC84C1BA08A6CC8E63FBBF22FB1D78A77AEAB'    # Giancarlo Razzolini
              'C100346676634E80C940FB9E9C02FF419FECBE16')   # Morten Linderud

prepare() {
  cd "$pkgname-$pkgver"
  local src
  for src in "${source[@]}"; do
      src="${src%%::*}"
      src="${src##*/}"
      [[ $src = *.patch ]] || continue
      echo "Applying patch $src..."
      patch -Np1 < "../$src"
  done
}

check() {
  make -C "$pkgname-$pkgver" check
}

package() {
  make -C "$pkgname-$pkgver" DESTDIR="$pkgdir" install
}
