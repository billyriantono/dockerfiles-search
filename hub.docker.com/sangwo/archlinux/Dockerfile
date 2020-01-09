FROM archlinux/base:latest

ENV MY_USERNAME=haoliang
ENV MY_PASSWD=xx

ARG MIRRORLIST
ENV MIRRORLIST=${MIRRORLIST:-mirrorlist}

COPY ./docker/config/$MIRRORLIST /etc/pacman.d/mirrorlist

# #{{{ 基本环境

# pacman -S base
RUN pacman -Syy --noconfirm \
    && pacman -S --noconfirm --needed \
    bash bzip2 coreutils \
    diffutils file filesystem findutils gawk gcc-libs glibc \
    grep gzip inetutils iproute2 iputils less licenses man-db man-pages \
    pacman perl procps-ng psmisc \
    sed shadow sysfsutils tar \
    util-linux which

# pacman -S base-devel
RUN pacman -Syy --noconfirm \
    && pacman -S --noconfirm --needed \
    autoconf automake binutils findutils \
    gcc groff \
    gzip libtool m4 make patch sudo \
    pkg-config fakeroot

# 本地化; local-gen requires glibc
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "zh_CN.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen

# git, curl
RUN pacman -Syy --noconfirm \
    && pacman -S --noconfirm --needed \
    git \
    curl

# #}}}

# normal user && cower #{{{
RUN pacman -Syy --noconfirm \
    && pacman -S --noconfirm --needed sudo
RUN echo '%wheel ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
RUN useradd -m -u 1000 -g users -G wheel $MY_USERNAME
RUN yes $MY_PASSWD | passwd $MY_USERNAME

USER $MY_USERNAME
RUN cd /tmp && git clone --depth 1 https://aur.archlinux.org/auracle-git.git \
    && cd auracle-git && makepkg -sirc --noconfirm --needed
COPY ./docker/scripts/cower_install.sh /usr/local/bin/cower_install.sh
USER root
# #}}}

# #{{{ 善后
RUN pacman -Syu --noconfirm

RUN pacman -Scc --noconfirm
RUN rm -rf /tmp/*
# #}}}
