FROM debian:stretch-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV MONO_VERSION 5.20.1.19

# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/etc/UTC /etc/localtime

# Use unicode
RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8

RUN apt-get -q update \
    && apt-get install -y gnupg

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch/snapshots/$MONO_VERSION main" > /etc/apt/sources.list.d/mono-official-stable.list \
    && apt-get -q update \
    && apt-get install -y \
    mono-devel \
    ca-certificates \
    ca-certificates-mono \
    fsharp \
    mono-vbnc \
    nuget \
    referenceassemblies-pcl \
    binutils \
    curl \
    dos2unix \
    git \
    rsync \
    sudo \
    tar \
    gzip \
    ssh \
    && rm -rf /var/lib/apt/lists/* /tmp/*

RUN groupadd --gid 3434 gitlabci \
    && useradd --uid 3434 --gid gitlabci --shell /bin/bash --create-home gitlabci \
    && echo 'gitlabci ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-gitlabci \
    && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep

USER gitlabci
