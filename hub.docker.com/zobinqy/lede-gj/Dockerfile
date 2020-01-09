FROM ubuntu:18.10
MAINTAINER zobinqy@163.com

RUN \
  apt-get update && \
  apt-get -y upgrade 
ENV DEBIAN_FRONTEND=noninteractive
RUN \
  apt-get install -y build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev && \
  apt-get install -y lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev && \
  apt-get install -y texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint gcc g++ bison && \
  apt-get install -y make sharutils ncurses-term gzip && \
  apt-get install -y wget curl && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
  dpkg-reconfigure -f noninteractive tzdata 
ENV FORCE_UNSAFE_CONFIGURE 1
