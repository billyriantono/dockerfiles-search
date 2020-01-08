FROM ubuntu:14.04

MAINTAINER Ivan Baranov "baranov.ivan.v@gmail.com"

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git-core gnupg flex bison gperf build-essential \
    zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 \
    lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache \
    libgl1-mesa-dev libxml2-utils xsltproc unzip \
    ca-certificates-java java-common libcups2 liblcms2-2 \
    libjpeg8 libnss3 libfreetype6 libpcsclite1 libxi6 \
    libxtst6 libxrender1 libgtk2.0-0 libxrandr2 libxinerama1 \
    libatk-wrapper-java-jni libasound2 libasound2 libgif4

RUN curl -o /tmp/jre-headless.deb "http://archive.ubuntu.com/ubuntu/pool/universe/o/openjdk-8/openjdk-8-jre-headless_8u45-b14-1_amd64.deb" && \
    dpkg -i /tmp/jre-headless.deb && \
    rm /tmp/jre-headless.deb && \
    curl -o /tmp/jre.deb "http://archive.ubuntu.com/ubuntu/pool/universe/o/openjdk-8/openjdk-8-jre_8u45-b14-1_amd64.deb" && \
    dpkg -i /tmp/jre.deb && \
    rm /tmp/jre.deb && \
    curl -o /tmp/jdk.deb "http://archive.ubuntu.com/ubuntu/pool/universe/o/openjdk-8/openjdk-8-jdk_8u45-b14-1_amd64.deb" && \
    dpkg -i /tmp/jdk.deb && \
    rm /tmp/jdk.deb

RUN mkdir /var/local/out && \
    export OUT_DIR_COMMON_BASE=/var/local/out