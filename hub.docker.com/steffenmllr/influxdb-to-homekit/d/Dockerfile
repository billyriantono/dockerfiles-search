FROM ubuntu:16.04

MAINTAINER ss8651twtw <ss8651twtw@gmail.com>

WORKDIR /root

# basic
RUN apt-get -qq update && \
    apt-get -qqy install vim \
    git \
    curl \
    wget \
    build-essential \
    socat \
    netcat \
    dnsutils \
    net-tools \
    nmap \
    nasm \
    hexedit \
    gdb \
    strace \
    ltrace \
    gcc-multilib \
    locales \
    ruby \
    ruby-dev \
    python \
    python-pip

# python package
RUN pip install pwntools && \
    pip install git+https://github.com/ReFirmLabs/binwalk.git

# peda and Pwngdb
RUN git clone https://github.com/longld/peda.git && \
    git clone https://github.com/scwuaptx/Pwngdb.git && \
    cp Pwngdb/.gdbinit .

# toolkit
RUN gem install one_gadget && \
    gem install seccomp-tools
