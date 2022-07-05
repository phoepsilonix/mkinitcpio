# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Dave Reisner <dreisner@archlinux.org>
# Maintainer: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=31
pkgrel=2.0
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://github.com/archlinux/mkinitcpio'
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod>=30' 'util-linux>=2.23' 'libarchive' 'coreutils'
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
        https://github.com/archlinux/mkinitcpio/pull/80.patch
        https://github.com/archlinux/mkinitcpio/pull/87.patch
        https://github.com/archlinux/mkinitcpio/pull/88.patch
        https://github.com/archlinux/mkinitcpio/pull/89.patch
        https://github.com/archlinux/mkinitcpio/pull/90.patch
        https://github.com/archlinux/mkinitcpio/pull/92.patch
        https://github.com/archlinux/mkinitcpio/pull/103.patch
        https://github.com/archlinux/mkinitcpio/pull/106.patch
        https://github.com/archlinux/mkinitcpio/pull/109.patch)
install=mkinitcpio.install
sha256sums=('8f2811250b852ab78375bf90e1a7430daa132e57e128b0f6eaadddd9b27bbc63'
            'SKIP'
            'b2627c0cefea71c185298487404464fdf4c208ffeb25608608d7e3b4313f7817'
            'dc57b5d5c09fb32d9cd87dd939ed867cd1fe78088fe5aa6d33c5512c86806e24'
            'aebf42b178ba89f50b20a62778c4844cd447241987fd27b3356b0bd241dd969a'
            '95fd044c9c696c90ccac71e6846bc8be29933481c49a861deb1de636b019dfde'
            '157cf6e07ae219fa0d4b805c077d48a2fdaa57220994c8e7b62320df9ea217e9'
            '8506058f6391820ffaf82453fdaf16e998781113e9d14fb06e3367ecc3caa0dc'
            '9adac6aca3a1ddd59c19a96eed905ecf89b36d2efec248c471d35445a5a7554f'
            'fa6edc0ed67169019726b8cc1c0dfd37ba313d4021dcf81faa239c472a102c5d'
            '968a53f45e70f09e28b0267710836ae1a5dc956ec9a1e74a9d13a36e4e2c9658'
            'b65cd5a4a410bd1049807025b2e2c50a23df4c79a42872fb09653db0ab1ae7ab'
            '4be2b899d6b96e18012dfaaebcaaf29d22b354b7b572fcde11c151676c85061c')
validpgpkeys=('ECCAC84C1BA08A6CC8E63FBBF22FB1D78A77AEAB')    # Giancarlo Razzolin

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
