# ArchLinux image with MinGW toolchain

FROM archlinux/base:latest
MAINTAINER tarmaciltur

# Locale
RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Update base system
RUN pacman -Syu --noconfirm --noprogressbar

# Enable multilib
RUN echo "[multilib]" >> /etc/pacman.conf && echo "Include = /etc/pacman.d/mirrorlist" >> /etc/pacman.conf 

# Add mingw-w64 repo
RUN    echo "[ownstuff]" >> /etc/pacman.conf \
    && echo "SigLevel = Optional TrustAll" >> /etc/pacman.conf \
    && echo 'Server = https://ftp.f3l.de/~martchus/$repo/os/$arch' >> /etc/pacman.conf \
    && echo 'Server = https://martchus.no-ip.biz/repo/arch/$repo/os/$arch' >> /etc/pacman.conf

#Build MinGW toolchain
RUN pacman -Syu --noconfirm base-devel mingw-w64-gcc

# Clean cache
RUN pacman -Scc --noconfirm

