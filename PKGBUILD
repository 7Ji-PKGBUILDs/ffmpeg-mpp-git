eval "$(curl -s -L https://raw.githubusercontent.com/hbiyik/agrrepo/refs/heads/master/libinherit/remote.sh)"
inherit https://github.com/archlinuxarm/PKGBUILDs/raw/master/extra/ffmpeg/

_ffmpeg_base=74e4393595cf2b5857f0da925c4e0dd74ea306e5
_ffmpeg_branch=9.1
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

build() {
  export PKG_CONFIG_PATH='/usr/lib/mbedtls2/pkgconfig'
  cd ffmpeg

  ./configure \
    --prefix=/usr \
    --disable-debug \
    --disable-static \
    --disable-stripping \
    --enable-amf \
    --enable-avisynth \
    --enable-cuda-llvm \
    --enable-fontconfig \
    --enable-frei0r \
    --enable-gmp \
    --enable-gnutls \
    --enable-gpl \
    --enable-ladspa \
    --enable-libaom \
    --enable-libass \
    --enable-libbluray \
    --enable-libbs2b \
    --enable-libdav1d \
    --enable-libdrm \
    --enable-libdvdnav \
    --enable-libdvdread \
    --enable-libfreetype \
    --enable-lcms2 \
    --enable-libfribidi \
    --enable-libgsm \
    --enable-libharfbuzz \
    --enable-libiec61883 \
    --enable-libjack \
    --enable-libjxl \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopenmpt \
    --enable-libopus \
    --enable-libplacebo \
    --enable-libpulse \
    --enable-librsvg \
    --enable-librubberband \
    --enable-libsnappy \
    --enable-libsoxr \
    --enable-libspeex \
    --enable-libsrt \
    --enable-libssh \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvidstab \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libwebp \
    --enable-libx264 \
    --enable-libx265 \
    --enable-libxcb \
    --enable-libxml2 \
    --enable-libxvid \
    --enable-libzimg \
    --enable-libzmq \
    --enable-opencl \
    --enable-shared \
    --enable-vapoursynth \
    --enable-version3 \
    --enable-vulkan \
    --disable-decoder=magicyuv \
    --enable-rkmpp \
    --enable-rkrga \
    --enable-pic
  make
  make tools/qt-faststart
  make doc/ff{mpeg,play}.1
}