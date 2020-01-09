# ArchLinux image with MinGW toolchain

FROM softwareperonista/archlinux-mingw-w64-doctrina:latest
MAINTAINER tarmaciltur

# Update base system
RUN pacman -Syu --noconfirm --noprogressbar

# Change user to build packages
USER devel
ENV TERM dumb
ENV MAKEFLAGS "-j8"

# Update AUR packages
RUN yay -Syu --noconfirm --noprogressbar

# Install needed packages
WORKDIR /home/devel
RUN wget https://aur.archlinux.org/cgit/aur.git/snapshot/mingw-w64-gstreamer.tar.gz
RUN bsdtar -xf mingw-w64-gstreamer.tar.gz
WORKDIR mingw-w64-gstreamer
RUN sed 's/${_arch}-meson/${_arch}-meson --buildtype plain/' -i PKGBUILD
RUN makepkg -si --noconfirm
WORKDIR /
#RUN yay -Syu --noconfirm mingw-w64-gstreamer
RUN yay -Syu --noconfirm mingw-w64-taglib
RUN yay -Syu --noconfirm mingw-w64-libsoup
RUN yay -Syu --noconfirm mingw-w64-gst-plugins-good

# Change user to root
USER root

# Clean cache
RUN pacman -Scc --noconfirm

