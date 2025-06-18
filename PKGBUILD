CONFIG="--enable-rkmpp --enable-rkrga"
eval "$(curl -s -L https://raw.githubusercontent.com/hbiyik/agrrepo/refs/heads/master/libinherit/remote.sh)"
inherit https://raw.githubusercontent.com/archlinuxarm/PKGBUILDs/master/extra/ffmpeg/

_ffmpeg_base=9373b442a689455bb5fcfddcfe70dfb8e4352fbc
_ffmpeg_branch=7.1
source+=("mpp.patch::https://github.com/nyanmisaka/ffmpeg-rockchip/compare/${_ffmpeg_base}...${_ffmpeg_branch}.patch")
b2sums+=("SKIP")
arch+=("aarch64" "arm7f")
replaces=("ffmpeg-mpp-git")
depends+=("mpp" "librga-multi")

_pkgname=ffmpeg-mpp
old_pkgname=$pkgname
pkgname=$_pkgname


prepare(){
  # patch with extra stuff
  cd $srcdir/ffmpeg
  patch -p1 -N -i ../mpp.patch
  cd $srcdir
  pkgname=$old_pkgname
  old_prepare
  pkgname=$_pkgname
}

build(){
  # pkgname is used in the build as variable so swap it
  pkgname=$old_pkgname
  old_build
  pkgname=$_pkgname
}

package(){
  # pkgname is used in the package as variable so swap it
  pkgname=$old_pkgname
  old_package
  pkgname=$_pkgname
}