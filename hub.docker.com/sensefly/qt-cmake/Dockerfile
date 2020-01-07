FROM sensefly/qt:xenial-5.11.2

ENV CMAKE_VERSION 3.12.2

WORKDIR /usr/src

RUN \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y \
    git \
    build-essential && \
  git clone git://cmake.org/cmake.git CMake && \
  cd CMake && \
  git checkout v$CMAKE_VERSION && \
  mkdir /usr/src/CMake-build && \
  cd /usr/src/CMake-build && \
  /usr/src/CMake/bootstrap \
    --parallel=$(grep -c processor /proc/cpuinfo) \
    --prefix=/usr && \
  make -j$(grep -c processor /proc/cpuinfo) && \
  ./bin/cmake \
    -DCMAKE_BUILD_TYPE:STRING=Release \
    -DBUILD_CursesDialog:BOOL=OFF \
    -DBUILD_QtDialog:BOOL=OFF \
    -DBUILD_TESTING:BOOL=OFF . && \
  make install && \
  cd .. && rm -rf CMake*

