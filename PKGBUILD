CONFIG="--enable-rkmpp --enable-rkrga --enable-pic"
eval "$(curl -s -L https://raw.githubusercontent.com/hbiyik/agrrepo/refs/heads/master/libinherit/remote.sh)"
inherit https://raw.githubusercontent.com/archlinuxarm/PKGBUILDs/master/extra/ffmpeg/

_ffmpeg_base=bf1b838f2ab88b4f8fd83443325c782ea0e0f7fa
_ffmpeg_branch=ffmpeg-rockchip-9.0.1
source+=("mpp.patch::https://github.com/hbiyik/ffmpeg-rockchip/compare/${_ffmpeg_base}...${_ffmpeg_branch}.patch")
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
