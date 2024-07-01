# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=39.2
pkgrel=2
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
        '0001-trigger.patch'
        # Manjaro patches
        'manjaro.patch'
        'manjaro-extramodules.patch'
        'manjaro-unsupported-modules_from_symbol.patch'
        )
install=mkinitcpio.install
sha512sums=('e4ba9fe901da56bb116510ec0c6abeba5153e57d9545baccbc466932951b7f324aa75ef7cc3de87f966456b0365b17552f367411d62585d500e88dc5c815058b'
            'SKIP'
            'b21e3961294e80bedd89a7e332ab11fc3b83eebfaf58d8f658e30f7d9caf2f84f4934224173c70f111932de8538fa327f5f6bfe9576b11bcbaf84d2d5ad8e85d'
            'ef6011509177276c79c35037ed305ca8c368ec7ee01f7f7a7ffa3abfd845a32f52d079627e0b1f22ad1b07d2eac1b5efb6ff74f9fa38440c7575ed47e2be0c37'
            '04f87d5aa3d159045cf25773f3113f9a875d20234ba736f429cdca3ca4f0cb08ee737792ae72ff7a00ac6573fe904cc030cc9adf0a6c5c8e319f370a33872317'
            '6928d41d93dfbb78f3a0f12230a3fb0e039fc1f074de7d147c2930b25316d10ea3dfd516f12b1eaabe8b508a95add3618beb22cf1fdbb374a5b02a0ebd1a4ae8')
b2sums=('7bd6bf491dd8b23d83e42834566375736cf8868d5120c7e24f4c8923eb03a64864cdda51d6a6f41373db88c29905535e4c8aa4bde172955bc7529e6b3ffc252c'
        'SKIP'
        '3b8e08d56e209ad11827d65595ab245bb680e72fb81139ba946e7610d16214c2a9022f1a1794e6797ef07fb0a43c5239167729225daf89396a8920f39f75e34b'
        '6698b916460b5c88b3c2b2494178afcee340f95453c6303ee5e4bce8cc53cc770f9f670d40c47f1f3b67a09c18b2ca06705de7021c85886475dd25367a478b3d'
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
