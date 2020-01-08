# Wayland compositor sway
#
# Run with x11docker: https://github.com/mviereck/x11docker
#     x11docker --gpu x11docker/sway
#
# sway on github:     https://github.com/swaywm/sway


FROM debian:buster

ENV PREFIX=/usr

RUN echo "deb http://deb.debian.org/debian experimental main" > /etc/apt/sources.list.d/experimental.list && \
    apt-get update && \
apt-get install -y \
    cmake \
    gcc \
    git \
    meson \
    pkg-config \
    universal-ctags && \
apt-get install -y -t experimental libjson-c4 libjson-c-dev scdoc && \
apt-get install -y \
    freerdp2-dev \
    libavcodec-dev \
    libavformat-dev \
    libavutil-dev \
    libcairo2-dev \
    libcap-dev \
    libdrm-dev \
    libegl1-mesa-dev \
    libelogind-dev \
    libgles2-mesa-dev \
    libgbm-dev \
    libgdk-pixbuf2.0-dev \
    libinput-dev \
    libpango1.0-dev \
    libpcre3-dev \
    libpixman-1-dev \
    libsystemd-dev \
    libwayland-dev \
    libudev-dev \
    libwinpr2-dev \
    libxcb-composite0-dev \
    libxcb-icccm4-dev \
    libxcb-xinput-dev \
    libxkbcommon-dev \
    wayland-protocols && \
cd /root && \
    git clone https://github.com/swaywm/wlroots.git && \
cd /root/wlroots && \
    meson build --prefix $PREFIX && \
    ninja -C build && \
    ninja -C build install && \
cd /root && \
    git clone https://github.com/swaywm/sway.git && \
cd /root/sway && \
    meson build --prefix $PREFIX && \
    ninja -C build && \
    ninja -C build install && \
apt-get remove -y \
    cmake \
    gcc \
    git \
    meson \
    pkg-config \
    universal-ctags \
    freerdp2-dev \
    libavcodec-dev \
    libavformat-dev \
    libavutil-dev \
    libcairo2-dev \
    libcap-dev \
    libdrm-dev \
    libegl1-mesa-dev \
    libelogind-dev \
    libgles2-mesa-dev \
    libgbm-dev \
    libgdk-pixbuf2.0-dev \
    libinput-dev \
    libjson-c-dev \
    libpango1.0-dev \
    libpcre3-dev \
    libpixman-1-dev \
    libsystemd-dev \
    libwayland-dev \
    libudev-dev \
    libwinpr2-dev \
    libxcb-composite0-dev \
    libxcb-icccm4-dev \
    libxcb-xinput-dev \
    libxkbcommon-dev \
    wayland-protocols && \
apt-get remove -y \
    libjson-c-dev && \
apt-get autoremove -y && apt-get clean && \
rm -R /root/* && \
apt-get install -y --no-install-recommends \
    libevdev2 \
    libinput10 \
    libfreerdp2-2 \
    libxkbcommon0 \
    libxcb-composite0 \
    libxcb-icccm4 \
    libxcb-xinput0 \
    libwayland-cursor0 \
    mesa-utils \
    mesa-utils-extra \
    xwayland && \
apt-get install -y --no-install-recommends \
    rxvt

# additional tools for tests, not needed for sway itself
#RUN apt-get install -y x11-xserver-utils x11-utils weston psmisc psutils procps

CMD sway
