FROM debian:jessie
MAINTAINER Kelvin You
USER root

ENV PATH="$PATH:/opt/brcm/hndtools-mipsel-linux/bin:/opt/brcm/hndtools-mipsel-uclibc/bin"

RUN apt-get update && \
    apt-get install -y vim git net-tools build-essential wget locales \
        libncurses5 libncurses5-dev m4 bison flex libtool sqlite \
        binutils patch bzip2 make gettext unzip zlib1g-dev \
        libc6 libncurses5-dev automake \
        libc6-i386 lib32z-dev gperf && \
    apt-get clean && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen && \
    ln -s /app/tools/brcm /opt/brcm
    
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

VOLUME "/app"
WORKDIR "/app"

CMD bash        
