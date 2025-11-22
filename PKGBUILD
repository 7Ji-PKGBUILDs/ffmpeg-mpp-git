CONFIG="--enable-rkmpp --enable-rkrga"
eval "$(curl -s -L https://raw.githubusercontent.com/hbiyik/agrrepo/refs/heads/master/libinherit/remote.sh)"
inherit https://raw.githubusercontent.com/archlinuxarm/PKGBUILDs/master/extra/ffmpeg/

_ffmpeg_base=44bfe0da6167c19221810f4865ba578e3ddd2c39
_ffmpeg_branch=8.0
source+=("mpp.patch::https://github.com/nyanmisaka/ffmpeg-rockchip/compare/${_ffmpeg_base}...${_ffmpeg_branch}.patch")
b2sums+=("SKIP")
arch+=("aarch64" "arm7f")
replaces=("ffmpeg-mpp-git")
provides+=("ffmpeg")
depends+=("mpp" "librga-multi")

pkgname=ffmpeg-mpp


prepare(){
  cd $srcdir
  old_prepare
  # patch with extra mpp stuff
  cd $srcdir/ffmpeg
  patch -p1 -N -i ../mpp.patch
}
