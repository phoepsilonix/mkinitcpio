# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=38
pkgrel=3
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
        'revert-ab6bad7.patch'
        )
install=mkinitcpio.install
sha512sums=('ad1a4895e5cc3a01637f71d96ddb79d7f45708ec7305ffdb874403a1eb3c1743d121f28d93273b91792298eb21bcc0c5d9ef1ab3a3773083d60da5bdaee59d6e'
            'SKIP'
            '32cf7e85aa09242a023712a05db74bfd765ea60e7a702a9c530b546360f835a71000f5d0fa0a10f504e53efcb46f0b38b09b55622c668440aafa6e7e00f616c7'
            '04f87d5aa3d159045cf25773f3113f9a875d20234ba736f429cdca3ca4f0cb08ee737792ae72ff7a00ac6573fe904cc030cc9adf0a6c5c8e319f370a33872317'
            '23160c5361fdc9338621917f533cedb05e416db05a52f63b18d4b544fbefe427925ea5e8c07f2191e8f248af4573aa814552f8f38de649e3933a2a9503220399'
            'f9d40d170fd6c7278252d61ab0018373b6b4dc3ed018f542a4745fd62e8ed2842e049c7ca8066b472fed1eafe1f19c4e6c167be2c5e3d61bb2bfdfd00782bc88')
b2sums=('4bc50da7196a69dc0ab7e7de345684baebbb655f9a07def9ac36a7f1c9aec752cf41c62134d6bbf240d8f49c6492a211f152bab062ec09457791d7ab030f1bc5'
        'SKIP'
        'a5fc389eb6611f9c149dbfd1fc0520a5d5d0a0d63367e498b70b38c1044d272df2fc4d484252b112a6757fea79a2f057943745cdd396f630ec71e4f6f45eecb8'
        '1046085788eea6ee04115d3776a292ae6e336fdc2f99b7a9ff4a6408e6b6a83cc106a41c46ba7fb795f81fcfa48ca1752ea3296f8d701435a49f7cbf107b8c76'
        '62bdbdc39f9837b322da789a6bd85b5801c6aabd667964e473b1a86a4d2d96d3c58b3829799bd21310d45c74e83f12e3ff93b2fd4bb1ebc1b42d23844ce71b5a'
        '44c66edefdce5836f57f272c86f90dd44c1669c0050efea01423e07856bb081466a1714dd31b41b159dcaaded38ffb175722db0297c76036303b380d94d76ea1')
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

