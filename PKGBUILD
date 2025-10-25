CONFIG="--enable-rkmpp --enable-rkrga"
eval "$(curl -s -L https://raw.githubusercontent.com/hbiyik/agrrepo/refs/heads/master/libinherit/remote.sh)"
inherit https://github.com/archlinuxarm/PKGBUILDs/raw/1c9c05cfaf861626e5409e19a551b177e4df3f1e/extra/ffmpeg

_ffmpeg_base=8f77695e65a69c8009804e9d457762d2d394403d
_ffmpeg_branch=7.1
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
