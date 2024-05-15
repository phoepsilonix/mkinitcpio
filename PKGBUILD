# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=38.1
pkgrel=2
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio'
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive' 'coreutils'
         'bash' 'binutils' 'diffutils' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'systemd')
makedepends=('asciidoc')
checkdepends=('bats' 'bats-assert' 'lzop')
optdepends=('zstd: Use zstd compression for the initramfs image'
            'xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
provides=('initramfs')
conflicts=(
  'systemd<255.4-2'
  'cryptsetup<2.7.0-3'
  'mdadm<4.3-2'
  'lvm2<2.03.23-3'
)
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.gz"{,.sig}
        # Manjaro patches
        'manjaro.patch'
        'manjaro-extramodules.patch'
        'manjaro-unsupported-modules_from_symbol.patch'
        #'revert-ab6bad7.patch'
        )
install=mkinitcpio.install
sha512sums=('e727509badc528f45f2b193b3f49c202df41d4e75067bebd44c22ebc59f635d4a9596bc671d609d8941644f3a246267f7a199946730ba474040a1f24b94f663c'
            'SKIP'
            'af940f543bb5fedcd17cbc42a38c652ccafdd25a1175b70b291dbcbf8c6e9fa4cf052aa905165eb8edb0f880ec255d67f5173f08d8e3635b15e3589a9803354a'
            '04f87d5aa3d159045cf25773f3113f9a875d20234ba736f429cdca3ca4f0cb08ee737792ae72ff7a00ac6573fe904cc030cc9adf0a6c5c8e319f370a33872317'
            '23160c5361fdc9338621917f533cedb05e416db05a52f63b18d4b544fbefe427925ea5e8c07f2191e8f248af4573aa814552f8f38de649e3933a2a9503220399')
b2sums=('625455bb1140688bcdf04c946eb6fa1da53deaa221b2c8090c173aef1d7fc617227aa0674344f3c18d5b9ab77a093725856f4f0cd3b8a33462a2ac742f0dbf11'
        'SKIP'
        '3a4e683e2ed97697d058c455e170e05559b64d61efbbd643baba4efb155ca32b9affd214025c73a6e210c4c4f17b5954447dabf7fbb3e1e31cf01f786aa14a04'
        '1046085788eea6ee04115d3776a292ae6e336fdc2f99b7a9ff4a6408e6b6a83cc106a41c46ba7fb795f81fcfa48ca1752ea3296f8d701435a49f7cbf107b8c76'
        '62bdbdc39f9837b322da789a6bd85b5801c6aabd667964e473b1a86a4d2d96d3c58b3829799bd21310d45c74e83f12e3ff93b2fd4bb1ebc1b42d23844ce71b5a')
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

