# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=37.1
pkgrel=3
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio'
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive' 'coreutils'
         'bash' 'binutils' 'diffutils' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'systemd')
#makedepends=('asciidoc')
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
        'test-use-system-library-loading-mechanism.patch'
        'https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio/-/merge_requests/292.patch'
        # Manjaro patches
        'manjaro.patch'
        'revert-ab6bad7.patch'
        )
install=mkinitcpio.install
sha512sums=('68fd36eb95317977dfb389be8bd1f6f09d455ca81b55cde8f64245fc59ceee74afa64b55dbb7e8b2e28abe8274397dbba2f4b021499f9ad6d662175ced678585'
            'SKIP'
            'c9a0dc49e7a22808f0556c79da3320edb93377d775c91343b2a1380aebde4e255b5e675e53a00192c73e4ea9a98a91b05b56c9d56d9e7537847274710115a6ae'
            'fccd46d7244d4749231bb366394f532a7de40bb3317740c5785f709818ad7c65fc3201b99c7b80533e3b96d86a5357a0d7c3301c8b5bb1c1b51da6d58c7dd15e'
            '2b374bca8449fb2154d4a314a209bbdd7cf95e34a2038e68ab8a666f657f141f0d73222636afb5c65daf44dee1a5a0a79975e2fc3d28daf8bab93ccfbc371214'
            'f9d40d170fd6c7278252d61ab0018373b6b4dc3ed018f542a4745fd62e8ed2842e049c7ca8066b472fed1eafe1f19c4e6c167be2c5e3d61bb2bfdfd00782bc88')
b2sums=('0b43d0d035fdba6195ca0e8facd654cbcff9c99d34d14b1f493c86cbea335c8f363e6117df7f0307e55b3e684fe7977d89ac226b79ed612270791e084b46aa4f'
        'SKIP'
        '11b8297ce18d47a0029490b950180801e5762ad7b7e36383d2f954cbc7aee10d3b901dd2703fd07b23b38aa6b74577b7d88a1d9eb5ff5633a665610c6fbec51b'
        'a1a0e84a737057aca3332dde5b114eaa918552afca2c627a7fb931b2d73f58e29819927c175fd25c846c6881f5efd895c57c32c8881d7e07a50de91fe449964a'
        '30802693fd01f7f08bdb0f028a4f68fd7033108c16ad37529f5b127c96c25a31c433d35dfb7764d063f8640f0df2f3aae5b29ae64423f871b7d36654d208ecc4'
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

