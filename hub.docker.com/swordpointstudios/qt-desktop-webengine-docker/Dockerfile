FROM ubuntu:18.04
MAINTAINER swordpointstudios <info@swordpointstudios.com>

ARG QT_VERSION=5.12.0

ENV DEBIAN_FRONTEND noninteractive
ENV QT_PATH /opt/Qt
ENV QT_DESKTOP $QT_PATH/${QT_VERSION}/gcc_64
ENV PATH $QT_DESKTOP/bin:$PATH

# Install updates & requirements:
#  * git, openssh-client, ca-certificates - clone & build
#  * locales, sudo - useful to set utf-8 locale & sudo usage
#  * curl - to download Qt bundle
#  * build-essential, pkg-config, libgl1-mesa-dev - basic Qt build requirements
#  * libsm6, libice6, libxext6, libxrender1, libfontconfig1, libdbus-1-3 - dependencies of the Qt bundle run-file
#  * libxi6, libgconf-2-4, libgtk-3-0, libx11-xcb1, libpq5, file - dependencies of the linuxdeployqt

RUN apt update && apt full-upgrade -y && apt install -y --no-install-recommends \
    git \
    openssh-client \
    ca-certificates \
    locales \
    sudo \
    curl \
    build-essential \
    pkg-config \
    libgl1-mesa-dev \
    libsm6 \
    libice6 \
    libxext6 \
    libxrender1 \
    libfontconfig1 \
    libdbus-1-3 \
    \
    libboost-all-dev \
    \
    libxi6 \
    libgconf-2-4 \
    libgtk-3-0 \
    libx11-xcb1 \
    libpq5 \
    file \
    libnss3 \
    libxtst6 \
    libasound2 \
    fuse \
    libfuse2 \
    \
    && apt-get -qq clean


COPY extract-qt-installer.sh install-linuxdeployqt.sh install-additional-qt-libs.sh /tmp/qt/

# Download & unpack Qt toolchains
# Download & unpack linuxdeployqt
# Download & unpack QtJsonSerializer
# Clean
RUN curl -Lo /tmp/qt/installer.run "https://download.qt.io/official_releases/qt/$(echo "${QT_VERSION}" | cut -d. -f 1-2)/${QT_VERSION}/qt-opensource-linux-x64-${QT_VERSION}.run" \
    && QT_CI_PACKAGES=qt.qt5.$(echo "${QT_VERSION}" | tr -d .).gcc_64,qt.qt5.$(echo "${QT_VERSION}" | tr -d .).qtnetworkauth,qt.qt5.$(echo "${QT_VERSION}" | tr -d .).qtremoteobjects,qt.qt5.$(echo "${QT_VERSION}" | tr -d .).qtwebglplugin,qt.qt5.$(echo "${QT_VERSION}" | tr -d .).qtwebengine,qt.qt5.$(echo "${QT_VERSION}" | tr -d .).qtscript /tmp/qt/extract-qt-installer.sh /tmp/qt/installer.run "$QT_PATH" \
    && find "$QT_PATH" -mindepth 1 -maxdepth 1 ! -name "${QT_VERSION}" -exec echo 'Cleaning Qt SDK: {}' \; -exec rm -r '{}' \; \
    && /tmp/qt/install-linuxdeployqt.sh "${QT_VERSION}" \
    && /tmp/qt/install-additional-qt-libs.sh "${QT_PATH}" "${QT_VERSION}" \
    && rm -rf /tmp/qt

# Reconfigure locale
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Add group & jenkins + sudo
RUN groupadd -g 1000 -r fuse && useradd --create-home --gid fuse jenkins && echo 'jenkins ALL=NOPASSWD: ALL' > /etc/sudoers.d/jenkins

USER jenkins
WORKDIR /home/jenkins
ENV HOME /home/jenkins
