FROM ubuntu:14.10
MAINTAINER TSUYUSATO Kitsune <make.just.on@gmail.com>

# install dependency packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get dist-upgrade -y
RUN apt-get install -y           \
      git                        \
      build-essential            \
      python                     \
      nasm                       \
      uuid-dev                   \
      iasl
ENV DEBIAN_FRONTEND interactive

# add user edk2
RUN useradd --create-home -s /bin/bash edk2 && \
    adduser edk2 sudo                       && \
    echo "edk2:edk2" | chpasswd
# edk2 is accpeted to execute sudo without password
RUN echo "Defaults:edk2 !authenticate" | tee /etc/sudoers.d/edk2

# set environment for edk2
USER edk2
ENV HOME /home/edk2
WORKDIR $HOME

# get and build EDK2 SDK
ADD /edk2 $HOME/edk2
RUN sudo chown edk2:edk2 -R $HOME/edk2
RUN cd $HOME/edk2 && make -C BaseTools

# execute bash
ADD /bashrc $HOME/.bashrc
ENV SHELL /bin/bash
CMD ["/bin/bash"]
