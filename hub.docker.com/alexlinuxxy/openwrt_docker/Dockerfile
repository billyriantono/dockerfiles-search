FROM alexlinuxxy/ubuntu_dev_docker
MAINTAINER Alex Huang "nikshuang@163.com"
ENV REFRESHED_AT 2016-7-26
RUN apt-get update
RUN apt-get install make libncurses5-dev libssl-dev gawk mawk autoconf automake zlib1g-dev xz-utils unzip bzip2 wget python2.7 subversion -y

RUN useradd -m docker
WORKDIR /home/docker
USER docker
RUN git clone https://github.com/openwrt/openwrt.git
COPY config openwrt/.config
RUN make -C openwrt oldconfig
