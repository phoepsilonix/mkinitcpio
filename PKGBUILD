# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=32
pkgrel=1
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://github.com/archlinux/mkinitcpio'
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive' 'coreutils'
         'bash' 'binutils' 'diffutils' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'systemd')
makedepends=('asciidoc')
optdepends=('xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'zstd: Use zstd compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
provides=('initramfs')
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.gz"{,.sig}
        # Manjaro patches
        manjaro.patch
        revert-ab6bad7.patch
        # Upstream PRs
        https://github.com/archlinux/mkinitcpio/pull/88.patch
        https://github.com/archlinux/mkinitcpio/pull/89.patch)
install=mkinitcpio.install
sha256sums=('f167d0b9831a5b6ae388525ebc92cea3a4766429e16ee2b56dbaa8d3b7c73ab2'
            'SKIP'
            'b2627c0cefea71c185298487404464fdf4c208ffeb25608608d7e3b4313f7817'
            'dc57b5d5c09fb32d9cd87dd939ed867cd1fe78088fe5aa6d33c5512c86806e24'
            '2d2814cf08a3afd0633967c3e7ad1df920318c028e97c46f4fbdb92a10f5f39a'
            'b59ea68a0ab205d169c0d71a631b0c40ec3a5af7a0596e7a8d6da59f6266c940')
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
