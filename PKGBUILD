# Maintainer: Calimero <calimeroteknik@free.fr>

pkgbase=linux-aufs_friendly  # Build kernel with a different name

# You can change pkgbase back to linux if you want to replace the one from [core].
#pkgbase=linux
# In this case, also uncomment this horrendous hack to complete the 'provides' array for aufs3
#depmod() { provides+=('aufs_friendly'); unset depmod; depmod "$@"; }

# Should be updated with the version of the kernel to build
pkgver=4.11.9

#Use the base branch:
#[[ "$pkgver" = *.*.* ]] && _kernel="${pkgver%.*}" || _kernel="${pkgver}"
# There is no patch for 4.11 only for 4.11.7+ (see: https://github.com/sfjro/aufs4-standalone/branches and http://aufs.sourceforge.net/)
_kernel=4.11.7+

pkgrel=1
arch=('i686' 'x86_64')
url='http://www.kernel.org/'
license=('GPL2')
pkgdesc='The aufs-compatible linux kernel and modules'
makedepends=('asp')
_source=("https://raw.githubusercontent.com/sfjro/aufs4-standalone/aufs${_kernel}/aufs4-base.patch"
         "https://raw.githubusercontent.com/sfjro/aufs4-standalone/aufs${_kernel}/aufs4-standalone.patch"
         "https://raw.githubusercontent.com/sfjro/aufs4-standalone/aufs${_kernel}/aufs4-mmap.patch"
         'add-aufs-patches.diff')
_md5sums=('SKIP'
          'SKIP'
          'SKIP'
          '268b9bf297431dbc66cb7827263f3d5e')
_sha256sums=('SKIP'
             'SKIP'
             'SKIP'
             '9a10dc166ef275fe5958bcc2523a47c35d642a17f18ce8aaaecde615ce1c474f')

## Fetch linux sources from ABS
if [ ! -d core-linux ];then
  ASPROOT=. asp checkout linux || exit 1
fi

# add AUFS patches
if [ ! -f linux/repos/core-${CARCH}/patched ];then
  patch -Np0 -i add-aufs-patches.diff || exit 1
  mv linux/repos/core-${CARCH}/PKGBUILD{,.core} || exit 1
  echo 'Do not remove this file: it indicates that these sources are patched for building an AUFS-friendly kernel.' > linux/repos/core-${CARCH}/patched
fi

# change the package basename to what's defined in this file
sed -i "s/^pkgbase=.*/pkgbase=${pkgbase}/" linux/repos/core-${CARCH}/PKGBUILD.core

# Hack for AUR package naming
pkgname="linux-aufs_friendly"

## Bootstrap build
cp linux/repos/core-${CARCH}/* .
source PKGBUILD.core

# Add AUFS patches' source URLs
source+=("${_source[@]}")
# Sometimes the maintainer feels like using md5, sometimes it's sha256
[[ "$md5sums" ]] && md5sums+=("${_md5sums[@]}")
[[ "$sha256sums" ]] && sha256sums+=("${_sha256sums[@]}")
