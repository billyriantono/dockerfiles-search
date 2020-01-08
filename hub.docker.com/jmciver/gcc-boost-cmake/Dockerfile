FROM gcc:latest

RUN apt-get -y update && apt-get -y install libboost-all-dev

RUN cd /root && \
  wget -q https://github.com/Kitware/CMake/releases/download/v3.14.0/cmake-3.14.0-Linux-x86_64.tar.gz && \
  tar xzf cmake-3.14.0-Linux-x86_64.tar.gz -C /usr/local --strip-components 1 && \
  rm cmake-3.14.0-Linux-x86_64.tar.gz

