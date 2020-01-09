FROM fedora:29
ARG FEDORA_VER=29

LABEL description="Fedora-based environment for building PipeWire" \
      maintainer="George Kiagiadakis <george.kiagiadakis@collabora.com>"

# Add rpmfusion repository for ffmpeg
RUN dnf install -y http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-${FEDORA_VER}.noarch.rpm \
    && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-${FEDORA_VER}-primary \
    && dnf upgrade -y \
    && dnf clean all

# Install pipewire dependencies
RUN dnf -y install \
    gcc \
    meson \
    systemd-devel \
    dbus-devel \
    glib-devel \
    gstreamer1-devel \
    gstreamer1-plugins-base-devel \
    jack-audio-connection-kit-devel \
    pulseaudio-libs-devel \
    alsa-lib-devel \
    libv4l-devel \
    libX11-devel \
    SDL2-devel \
    libva-devel \
    bluez-libs-devel \
    sbc-devel \
    speexdsp-devel \
    ffmpeg-devel \
    doxygen \
    graphviz \
    xmltoman \
    git \
    make \
    findutils \
    && dnf clean all

CMD ["/bin/bash"]
