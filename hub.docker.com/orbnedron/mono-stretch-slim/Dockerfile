FROM debian:stretch-slim
MAINTAINER orbnedron

# Other Arguments
ARG DEBIAN_FRONTEND=noninteractive

# Install mono
RUN apt-get update -q \
    && apt-get install -qy gnupg2 \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
    && echo "deb http://download.mono-project.com/repo/debian stable-stretch main" > /etc/apt/sources.list.d/mono-official-stable.list \
    && apt-get update -q \
    && apt-get install -qy libmono-cil-dev ca-certificates-mono \
    && apt-get -y autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/tmp/* \
    && rm -rf /tmp/*
