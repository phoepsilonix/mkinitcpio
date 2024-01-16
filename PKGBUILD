# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=37.2
pkgrel=1.1
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
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.gz"{,.sig}
        # Manjaro patches
        'manjaro.patch'
        'manjaro-extramodules.patch'
        'revert-ab6bad7.patch'
        )
install=mkinitcpio.install
sha512sums=('66a608857e845de92ca15e14787e413a343f1cf3480d2fa09daa85f71cb03c3d3cf1171c46de9d788baf7e34c8233df324a442529d9ce477b13c16dd09465fb9'
            'SKIP'
            '2b374bca8449fb2154d4a314a209bbdd7cf95e34a2038e68ab8a666f657f141f0d73222636afb5c65daf44dee1a5a0a79975e2fc3d28daf8bab93ccfbc371214'
            '33ad81a2861afd0ced93c0ef5962c1db55e76f87f0a173a011a6ebb8e053219a1d962a98157238b7209cbcf8539a5a4f950ec1855efc948c9cc84fc8f0f01007'
            'f9d40d170fd6c7278252d61ab0018373b6b4dc3ed018f542a4745fd62e8ed2842e049c7ca8066b472fed1eafe1f19c4e6c167be2c5e3d61bb2bfdfd00782bc88')
b2sums=('9d1b36445c48db7317cb41b50e2dc0233104180cb4dbd649a81a83e3da8db3ac66e45ef5a023fb6be03841018a2fca139bdfda336a509e96148f4d6f57ff7818'
        'SKIP'
        '30802693fd01f7f08bdb0f028a4f68fd7033108c16ad37529f5b127c96c25a31c433d35dfb7764d063f8640f0df2f3aae5b29ae64423f871b7d36654d208ecc4'
        '5d809fba061f2f1d96f5d0921c60a58114422a6e87b78e3f6f086ed813cbf37df2b2ebc18386c4a9656dcdbf676521a59eb062c8d39fbe59bb980b0c85322ada'
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

