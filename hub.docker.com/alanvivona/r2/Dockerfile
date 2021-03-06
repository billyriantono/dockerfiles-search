# Custom r2 docker build 
# ========
# ubuntu
# nodejs
# python pip
# r2
# r2pipe
# r2frida
# r2dec
#
# Takes your custom config file (.radare2rc) from the current directory
# Copies contents of ./data to /home/r2/data
#
# Build docker image with:
# $ docker build -t r2-docker:latest .
#
# Open binary with frida:
# r2 frida:/home/r2/data/sample


# Using Ubuntu latest as base image.
FROM ubuntu:latest

# Label base
LABEL r2-docker latest

# Build and install radare2 on master branch
RUN DEBIAN_FRONTEND=noninteractive dpkg --add-architecture i386 && apt-get update

# Build dependencies
RUN apt-get install -y \
  curl \
  gcc \
  git \
  bison \
  pkg-config \
  make \
  glib-2.0 \
  libc6:i386 \
  libncurses5:i386 \
  libstdc++6:i386 \
  gnupg2 \
  sudo \
  xz-utils \
  python-pip \
  openssl \
  build-essential \
  xxd

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update
RUN apt-get install nodejs

# r2pipe
RUN pip install r2pipe && npm install --unsafe-perm -g r2pipe

# r2
RUN git clone -q --depth 1 https://github.com/radare/radare2.git && \
    ./radare2/sys/install.sh
  
# Create non-root user
RUN useradd -m r2 && adduser r2 sudo && echo "r2:r2" | chpasswd

# Initilise base user
USER r2
WORKDIR /home/r2
ENV HOME /home/r2

# Setup r2pm
RUN r2pm init && r2pm update && chown -R r2:r2 /home/r2/.config

# r2dec plugin
# command pdd
# .radare2rc options:
#   r2dec.casts         | if false, hides all casts in the pseudo code.
#   r2dec.asm           | if true, shows pseudo next to the assembly.
#   r2dec.blocks        | if true, shows only scopes blocks.
#   r2dec.paddr         | if true, all xrefs uses physical addresses compare.
#   r2dec.xrefs         | if true, shows all xrefs in the pseudo code.
#   r2dec.theme         | defines the color theme to be used on r2dec.
#   e scr.html          | outputs html data instead of text.
#   e scr.color         | enables syntax colors.
RUN r2pm -ci r2dec

# r2frida plugin
# Forms of use:
# $ r2 frida://Twitter
# $ r2 frida://1234
# $ r2 frida:///bin/ls
# $ r2 frida://"/bin/ls -al"
# $ r2 frida://device-id/Twitter
RUN r2pm -ci r2frida

# Cleanup
USER root
RUN apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Base command for container
USER r2
COPY .radare2rc /home/r2/.radare2rc
COPY ./data /home/r2/data

ENTRYPOINT bash