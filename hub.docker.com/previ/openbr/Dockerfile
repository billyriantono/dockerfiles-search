FROM previ/opencv:latest 
 
MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /tmp/downloads

RUN sudo apt-get install -y git qt5-default libqt5svg5-dev qtcreator

RUN git clone http://github.com/biometrics/openbr.git && \
      cd openbr && \
      git checkout v1.1.0 && \
      git submodule init && \
      git submodule update

RUN cd openbr && mkdir build && \
      cd build && \
      cmake -DCMAKE_BUILD_TYPE=RELEASE -DBR_INSTALL_BRPY=ON .. && \
      make -j4 && \
      sudo make install && \
      cd ../.. && \
      rm -rf openbr*

