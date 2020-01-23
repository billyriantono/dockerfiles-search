FROM ubuntu:latest
MAINTAINER Luca Borzacchiello <lucaborza@gmail.com>

# Environments vars
ENV TERM=xterm

RUN apt-get update
RUN apt-get -y upgrade

# Packages installation
RUN DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing install \
      sudo \
      git \
      curl \
      vim \
      build-essential \
      gcc-multilib \
      z3 \
      libz3-dev \
      gdbserver \
      tmux

# user
RUN adduser klee-native && \
    echo "klee-native ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/klee-native && \
    chmod 0440 /etc/sudoers.d/klee-native
USER klee-native
WORKDIR /home/klee-native

# remill
RUN git clone https://github.com/trailofbits/remill.git

# klee
RUN cd remill/tools && \
    git clone https://github.com/trailofbits/klee.git && \
    cd ../../ && \
    echo "set(CMAKE_BUILD_TYPE Debug)" >> ./remill/tools/klee/CMakeLists.txt

# build
RUN ./remill/scripts/build.sh --llvm-version 7.0 --use-host-compiler && \
    cd remill-build && \
    sudo make install && \
    cd ..

# bin folder
RUN mkdir bin && \
    ln -s /home/klee-native/remill-build/tools/klee/klee-snapshot-7.0 /home/klee-native/bin && \
    ln -s /home/klee-native/remill-build/tools/klee/klee-exec-7.0 /home/klee-native/bin
RUN echo "export PATH=$PATH:/home/klee-native/bin" >> .bashrc

# configs
RUN echo "set number" >> /home/klee-native/.vimrc

# script
COPY copy_to_shared.sh /home/klee-native/copy_to_shared.sh
