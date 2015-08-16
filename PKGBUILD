# Contributor: Michael Egger <gcarq at-symbol archlinux . info>

# toolchain build order: linux-api-headers->glibc->binutils->gcc->binutils->glibc

_target_arch=mipsel
_target=${_target_arch}-linux-gnu
pkgname=${_target}-linux-api-headers
pkgver=3.19
_basever=3.19
pkgrel=1
pkgdesc="Kernel headers sanitized for use in userspace (${_target})"
arch=(any)
url="http://www.gnu.org/software/libc"
license=('GPL2')
provides=("${_target}-linux-api-headers=${_basever}"
  "${_target}-linux-api-headers30")
conflicts=("${_target}-linux-api-headers26")
source=("http://www.kernel.org/pub/linux/kernel/v3.x/linux-${pkgver}.tar.xz")
md5sums=('d3fc8316d4d4d04b65cbc2d70799e763')

build() {
  cd "${srcdir}/linux-${pkgver}"

  make ARCH=${_target_arch} mrproper
  make ARCH=${_target_arch} headers_check
}

package() {
  cd "${srcdir}/linux-${pkgver}"

  make INSTALL_HDR_PATH="${pkgdir}/usr/${_target}/" ARCH=${_target_arch} V=0 \
    headers_install

  # use headers from libdrm
  #rm -rf ${pkgdir}/usr/include/drm
  # clean-up unnecessary files generated during install
  find "${pkgdir}" -name .install -or -name ..install.cmd | xargs rm -f
}
