# ArchLinux image with MinGW toolchain

FROM softwareperonista/archlinux-mingw-w64:latest
MAINTAINER tarmaciltur

# Update base system
RUN pacman -Syu --noconfirm --noprogressbar

# Install needed packages
RUN pacman -Syu --noconfirm --noprogressbar gtk3 mingw-w64-gtk3

# Clean cache
RUN pacman -Scc --noconfirm
