# Maintainer: Mahmut Dikcizgi <boogiepop a~t gmx com>
# Contributor: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

# ALARM: Kevin Mihelich <kevin@archlinuxarm.org>
#  - use -fPIC in host cflags for v7/v8 to fix print_options.c compile
#  - remove makedepends on ffnvcodec-headers, remove --enable-nvenc, --enable-nvdec
#  - remove depends on aom, remove --enable-libaom
#  - remove depends on intel-media-sdk, remove --enable-libmfx
#  - remove depends on vmaf, remove --enable-vmaf
#  - remove depends on rav1e, remove --enable-librav1e
#  - remove depends on svt-av1, remove --enable-libsvtav1
#  - remove --enable-lto
#  - enable rockchip decoders witht he highest priority
#  - interface rockchip rga from kernel to userspace directly
#  - hack around rockchips vp8&9 colorspace is not detected when used with Firefox

pkgname=ffmpeg-mpp-git
pkgver=7.1.r117254.dc1e883921
pkgrel=1
_obs_deps_tag=2023-04-03
_github_user=nyanmisaka
_github_repo=ffmpeg-rockchip
_github_branch=7.1
pkgdesc='Complete solution to record, convert and stream audio and video supporting rockchip MPP hardware decoder'
arch=(aarch64 armv7h)
url="https://github.com/$_github_user/$_github_repo.git"
license=(GPL3)
options=(!lto strip)
depends=(
  alsa-lib
  bzip2
  cairo
  dav1d
  fontconfig
  freetype2
  fribidi
  glib2
  glibc
  gmp
  gsm
  harfbuzz
  jack
  lame
  libass
  libavc1394
  libbluray
  libbs2b
  libdrm
  libdvdnav
  libdvdread
  libgl
  libiec61883
  libjxl
  libmodplug
  libopenmpt
  libplacebo
  libpulse
  libraw1394
  librsvg
  libsoxr
  libssh
  libtheora
  libva
  libvdpau
  libvorbis
  libvpx
  libwebp
  libx11
  libxcb
  libxext
  libxml2
  libxv
  mbedtls2
  ocl-icd
  opencore-amr
  openjpeg2
  opus
  rubberband
  sdl2
  snappy
  speex
  srt
  v4l-utils
  vapoursynth
  vid.stab
  vulkan-icd-loader
  x264
  x265
  xvidcore
  xz
  zimg
  zlib
  mpp
  librist
  librga-multi
)
makedepends=(
  amf-headers
  avisynthplus
  clang
  frei0r-plugins
  git
  ladspa
  mesa
  nasm
  opencl-headers
  vulkan-headers
  mpp
  perl
  gitweb-dlagent
)

optdepends=(
  'avisynthplus: AviSynthPlus support'
  'frei0r-plugins: Frei0r video effects support'
  'ladspa: LADSPA filters'
)

provides=(
  libavcodec.so
  libavdevice.so
  libavfilter.so
  libavformat.so
  libavutil.so
  libpostproc.so
  libswresample.so
  libswscale.so
  "ffmpeg=${pkgver}-${pkgrel}"
  "ffmpeg-obs=${pkgver}-${pkgrel}"
  "ffmpeg-rockchip"
  "ffmpeg-rockchip-git"
)

conflicts=(
  ffmpeg
  $pkgname
)

# to prevent multiple previous ffmpeg packages colliding
replaces=(
  ffmpeg-rockchip
  ffmpeg-rockchip-git
)

DLAGENTS+=('gitweb-dlagent::/usr/bin/gitweb-dlagent sync %u')
_url_ffmpeg="gitweb-dlagent://github.com/$_github_user/$_github_repo#branch=$_github_branch"

source=(
  "$_url_ffmpeg"
  "obs-deps::git+https://github.com/obsproject/obs-deps.git#tag=${_obs_deps_tag}"
  add-av_stream_get_first_dts-for-chromium.patch
)

b2sums=('SKIP'
        'SKIP'
        '555274228e09a233d92beb365d413ff5c718a782008075552cafb2130a3783cf976b51dfe4513c15777fb6e8397a34122d475080f2c4483e8feea5c0d878e6de')

validpgpkeys=(DD1EC9E8DE085C629B3E1846B18E8928B3948D64) # Michael Niedermayer <michael@niedermayer.cc>

prepare() {
  cd ffmpeg-rockchip
  sed -i 's/RTLD_LOCAL/RTLD_DEEPBIND/g' libavformat/avisynth.c
  patch -Np1 -i ../add-av_stream_get_first_dts-for-chromium.patch # https://crbug.com/1251779
  
  # This patch applies:
  #  - Fix decoding of certain malformed FLV files
  #  - Add additional CPU levels for libaom
  patch -Np1 -i ../obs-deps/deps.ffmpeg/patches/FFmpeg/0001-flvdec-handle-unknown.patch
  patch -Np1 -i ../obs-deps/deps.ffmpeg/patches/FFmpeg/0002-libaomenc-presets.patch
}

pkgver() {
  cd ffmpeg-rockchip
  local _rev=$(gitweb-dlagent version ${_url_ffmpeg} --pattern \{revision\})
  local _com=$(gitweb-dlagent version ${_url_ffmpeg} --pattern \{commit:.10s\})
  printf "%s.r%s.%s" "$(cat RELEASE)" $_rev $_com
}

build() {
  export PKG_CONFIG_PATH='/usr/lib/mbedtls2/pkgconfig'
  cd ffmpeg-rockchip
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
    --enable-gpl \
    --enable-ladspa \
    --enable-libass \
    --enable-libbluray \
    --enable-libbs2b \
    --enable-libdav1d \
    --enable-libdrm \
    --enable-libdvdnav \
    --enable-libdvdread \
    --enable-libfreetype \
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
    --enable-mbedtls \
    --enable-opencl \
    --enable-opengl \
    --enable-shared \
    --enable-vapoursynth \
    --enable-version3 \
    --enable-librist \
    --disable-vulkan \
    --disable-doc \
    --enable-rkmpp \
    --enable-rkrga  $CONFIG
  make ${MAKEFLAGS}
  make ${MAKEFLAGS} tools/qt-faststart
  make ${MAKEFLAGS} doc/ff{mpeg,play}.1
}

package() {
  make ${MAKEFLAGS} DESTDIR="${pkgdir}" -C ffmpeg-rockchip install install-man
  install -Dm 755 ffmpeg-rockchip/tools/qt-faststart "${pkgdir}"/usr/bin/
}
