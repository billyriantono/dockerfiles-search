# Check http://releases.llvm.org/download.html#7.0.1 for the latest available binaries
FROM ubuntu:18.04

# Make sure the image is updated, install some prerequisites,
# Download the latest version of Clang (official binary) for Ubuntu
# Extract the archive and add Clang to the PATH
RUN apt-get update && apt-get install -y \
  xz-utils zip gzip tar \
  build-essential \
  gcc-8 \
  g++-8 \
  curl \
  ninja-build \
  git \
  python2.7 \
  && ln -s /usr/bin/python2.7 /usr/bin/python \
  && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 700 --slave /usr/bin/g++ g++ /usr/bin/g++-7 \
  && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 800 --slave /usr/bin/g++ g++ /usr/bin/g++-8 \
  && rm -rf /var/lib/apt/lists/* \
  && curl -SL http://releases.llvm.org/7.0.1/clang+llvm-7.0.1-x86_64-linux-gnu-ubuntu-18.04.tar.xz | tar -xJC . \
  && cp -R clang+llvm-7.0.1-x86_64-linux-gnu-ubuntu-18.04/* /usr/local/ \
  && curl -SL https://nodejs.org/dist/v10.15.0/node-v10.15.0-linux-x64.tar.xz | tar -xJC . \
  && cp -R node-v10.15.0-linux-x64/* /usr/local/ \
  && curl -SL https://github.com/Kitware/CMake/releases/download/v3.13.3/cmake-3.13.3-Linux-x86_64.tar.gz | tar xvz -C . \
  && rm -rf /usr/local/man \
  && cp -rf cmake-3.13.3-Linux-x86_64/* /usr/local/

#CMD [ "" ]
