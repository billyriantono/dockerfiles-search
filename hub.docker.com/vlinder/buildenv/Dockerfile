FROM ubuntu:xenial

# make sure we're up-to-date
RUN apt-get -y update && apt-get -y upgrade 

# set the locale
RUN apt-get -y install locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# install everything we need for Yocto builds
RUN apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm

# Add Boost
RUN wget https://dl.bintray.com/boostorg/release/1.70.0/source/boost_1_70_0.tar.bz2
RUN tar xjvf boost_1_70_0.tar.bz2
WORKDIR boost_1_70_0
RUN ./bootstrap.sh --prefix=/usr
RUN ./b2 --without-python
RUN ./b2 --without-python install
WORKDIR ..
RUN rm -fr boost_1_70_0
RUN rm boost_1_70_0.tar.bz2

# add libsodium
RUN wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz
RUN tar xzf LATEST.tar.gz
WORKDIR libsodium-stable
RUN ./configure --prefix=/usr
RUN make
RUN make install
WORKDIR ..
RUN rm -fr libsodium-stable
RUN rm LATEST.tar.gz

