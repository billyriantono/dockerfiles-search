FROM ubuntu:14.04
MAINTAINER Luca Borzacchiello <lucaborza@gmail.com>

# Environments vars
ENV TERM=xterm

RUN apt-get update
RUN apt-get -y upgrade

# Packages installation
RUN DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing install git \
      subversion \
      build-essential \
      automake \
      binutils-dev \
      libiberty-dev \
      zlib1g-dev \
      ocaml \
      ocaml-findlib \
      libextlib-ocaml-dev \
      build-essential \
      valgrind \
      qemu \
      binutils-multiarch \
      binutils-dev \
      libgdome2-ocaml-dev \
      camlidl \
      ocaml-native-compilers \
      libocamlgraph-ocaml-dev \
      libsqlite3-ocaml-dev \
      subversion \
      libgmp3-dev \
      zsh \
      automake \
      bison \
      flex \
      cmake \
      libboost-system-dev \
      libboost-program-options-dev

# user
RUN adduser fuzzball
USER fuzzball
WORKDIR /home/fuzzball

# valgrind
RUN git clone https://github.com/bitblaze-fuzzball/valgrind-vex-for-fuzzball.git && \
    cd valgrind-vex-for-fuzzball/VEX && \
    make -f Makefile-gcc EXTRA_CFLAGS=-std=c99

# stp
RUN git clone https://github.com/bitblaze-fuzzball/stp && \
    cd stp && \
    mkdir build && \
    cd build && \
    cmake -G 'Unix Makefiles' .. && \
    make

# fuzzball
RUN git clone https://github.com/bitblaze-fuzzball/fuzzball.git && \
    cp /home/fuzzball/stp/build/stp /home/fuzzball/fuzzball/stp && \
    cp /home/fuzzball/stp/build/lib/libstp.a /home/fuzzball/fuzzball/stp && \
    cd fuzzball && \
    ./autogen.sh && \
    ./configure --with-vex=/home/fuzzball/valgrind-vex-for-fuzzball/VEX/ && \
    make

# bin folder
RUN mkdir bin && \
    ln -s /home/fuzzball/fuzzball/exec_utils/fuzzball /home/fuzzball/bin && \
    ln -s /home/fuzzball/fuzzball/exec_utils/test_insn /home/fuzzball/bin && \
    ln -s /home/fuzzball/fuzzball/exec_utils/vinegrind /home/fuzzball/bin && \
    ln -s /home/fuzzball/stp/build/stp /home/fuzzball/bin

RUN echo "export PATH=$PATH:/home/fuzzball/bin" >> .bashrc
