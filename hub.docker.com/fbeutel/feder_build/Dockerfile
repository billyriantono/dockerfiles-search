FROM fedora:latest
MAINTAINER Fabian Beutel

RUN dnf install -y \
        gcc \
        gcc-c++ \
        cmake \
        make \
        lcov \
        pkgconfig \
        openssl \
        qt5-qtbase-devel \
        qt5-qtdeclarative-devel \
        glib2-devel \
        gstreamer1-devel \
        gstreamer1-plugins-base \
        gstreamer1-plugins-good \
        libnice-devel \
        libnice-gstreamer1 \
    && dnf -y clean all
    
WORKDIR /opt/workdir
