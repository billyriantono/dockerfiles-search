FROM jforissier/optee_os_ci
MAINTAINER Jerome Forissier <jerome.forissier@linaro.org>

RUN dpkg --add-architecture i386

RUN apt-get update \
 && apt-get install -y \
  android-tools-adb \
  android-tools-fastboot \
  autoconf \
  automake \
  bc \
  bison \
  build-essential \
  ccache \
  cscope \
  curl \
  device-tree-compiler \
  flex \
  ftp-upload \
  gdisk \
  iasl \
  libattr1-dev \
  libc6:i386 \
  libcap-dev \
  libfdt-dev \
  libftdi-dev \
  libglib2.0-dev \
  libhidapi-dev \
  libncurses5-dev \
  libpixman-1-dev \
  libssl-dev \
  libstdc++6:i386 \
  libtool \
  libz1:i386 \
  make \
  mtools \
  netcat \
  python-crypto \
  python-serial \
  python-wand \
  unzip \
  uuid-dev \
  xdg-utils \
  xterm \
  xz-utils \
  zlib1g-dev \
 && apt-get autoremove

