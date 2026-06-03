CONFIG="--enable-rkmpp --enable-rkrga --enable-pic"
eval "$(curl -s -L https://raw.githubusercontent.com/hbiyik/agrrepo/refs/heads/master/libinherit/remote.sh)"
inherit https://raw.githubusercontent.com/archlinuxarm/PKGBUILDs/master/extra/ffmpeg/

_ffmpeg_base=7f5c90f77e1f63a6aa340db4a4aa7742f81a61cb
_ffmpeg_branch=8.1
source+=("mpp.patch::https://github.com/nyanmisaka/ffmpeg-rockchip/compare/${_ffmpeg_base}...${_ffmpeg_branch}.patch")
b2sums+=("SKIP")
arch+=("aarch64" "arm7f")
replaces=("ffmpeg-mpp-git")
provides+=("ffmpeg")
conflicts+=("ffmpeg")
depends+=("mpp" "librga-multi")
options=(!lto)

pkgname=ffmpeg-mpp


prepare(){
  cd $srcdir
  old_prepare
  # patch with extra mpp stuff
  cd $srcdir/ffmpeg
  patch -p1 -N -i ../mpp.patch
}
