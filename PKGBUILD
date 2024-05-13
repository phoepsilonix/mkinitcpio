# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=39.1
pkgrel=1
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
sha512sums=('8d6ed6eb222f34960e5cd9480e965f1fdb9b1af439d68e199cd17e92a3bbc8a34fb9d4ade1b32a3f8b844529b1c6fbeb2d2fa40e0cf9bd1dd767caa2bb148b60'
            'SKIP'
            'cab3e6ff8d484ff2fda028f37695d8329c13aa240fe13dd1640a05d0147744c20c284cf30fc1079dac54a9813caf5fcbbac78342350305148462738132b350aa'
            '04f87d5aa3d159045cf25773f3113f9a875d20234ba736f429cdca3ca4f0cb08ee737792ae72ff7a00ac6573fe904cc030cc9adf0a6c5c8e319f370a33872317'
            '6928d41d93dfbb78f3a0f12230a3fb0e039fc1f074de7d147c2930b25316d10ea3dfd516f12b1eaabe8b508a95add3618beb22cf1fdbb374a5b02a0ebd1a4ae8')
b2sums=('f3ac6e73dcb3825f6708a97022a7573078d9ac11bd5f7f147dc6dabfbe406fb56157cf0efef126b0e505b22816257c329d809f1bc085724ad305928137be9248'
        'SKIP'
        'f60eb492a9c37bea362c7dbab0b1342710a5c675fa7c3c29a65649fbd6449aba239b307f7778cf0184bc2b477db29fabb1867d88e635603f274e6c77dae0b991'
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
