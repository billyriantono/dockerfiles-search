FROM i386/debian:buster

LABEL maintainer="Denis Tulyakov <dtulyakov@gmail.com>" \
  org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.docker.cmd="docker run --rm -it -v \${PWD}:/app nkbvs/debian-10_i386_cpp_base bash" \
  org.label-schema.description="Debian C++ builder" \
  org.label-schema.name="debian-10_i386_cpp_base" \
  org.label-schema.schema-version="10" \
  org.label-schema.url="https://debian.org" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://bitbucket.org/nkbvs/docker-debian-10_i386_cpp_base" \
  org.label-schema.vendor="dtulyakov" \
  org.label-schema.version=$VERSION

ENV DEBIAN_FRONTEND="noninteractive"

USER root

RUN set -x \
  && apt-get update -qq \
  && apt-get install -qy \
     autoconf \
     automake \
  && apt-get install -qy \
     bash-completion \
     build-essential \
     bzip2 \
     ca-certificates \
     clang \
     clang-tidy \
     cmake \
     cmake-curses-gui \
     curl \
     debhelper \
     dh-systemd \
     fakeroot \
     gdbserver \
#     git \
     git-buildpackage \
     gnupg2 \
     libasio-dev \
     libblkid-dev \
     libboost-all-dev \
     libcap-dev \
     libeigen3-dev \
     libgeographic-dev \
     libgles2-mesa-dev \
     libglib2.0-dev \
     libgtest-dev \
     libjemalloc-dev \
     libjson-c-dev \
     liblog4cxx-dev \
     liblz4-dev \
     libmount-dev \
     libncurses-dev \
     libncursesw5-dev \
     libopencv-dev \
     libpcre3-dev \
     libpstreams-dev \
     libqt4-dev \
     libsystemd-dev \
     libtinyxml2-dev \
     libtinyxml2.6.2v5 \
     libtool \
     libtclap-dev \
     libudev-dev \
     libusb-1.0-0-dev \
     libva-dev \
     libxinerama-dev \
     libxtst-dev \
     libyaml-cpp-dev \
     libzzip-dev \
#     linux-headers-$(uname -r) \
     llvm \
     llvm-dev \
     lsb-release \
     net-tools \
#     openssl \
     pkg-config \
     python-dev \
     python3-pip \
     python3-setuptools \
     qt5-default \
     rapidjson-dev \
     software-properties-common \
     unzip \
     usbutils \
     valgrind \
     vim \
     wget \
     zlib1g-dev \
  && apt-get autoremove -y \
  && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/* /var/lib/apt/lists/*


# vim: set filetype=dockerfile et sw=2 ts=2:
