FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
  xz-utils \
  zip gzip tar \
  build-essential \
  curl \
  ninja-build \
  libxml2 \
  git \
  python2.7 \
  && ln -s /usr/bin/python2.7 /usr/bin/python \
  && rm -rf /var/lib/apt/lists/* \
  && curl -SL http://releases.llvm.org/7.0.1/clang+llvm-7.0.1-x86_64-linux-gnu-ubuntu-18.04.tar.xz | tar -xJC . \
  && cp -R clang+llvm-7.0.1-x86_64-linux-gnu-ubuntu-18.04/* /usr/local/ \
  && curl -SL https://nodejs.org/dist/v10.15.0/node-v10.15.0-linux-x64.tar.xz | tar -xJC . \
  && cp -R node-v10.15.0-linux-x64/* /usr/local/ \
  && curl -SL https://github.com/Kitware/CMake/releases/download/v3.13.3/cmake-3.13.3-Linux-x86_64.tar.gz | tar xvz -C . \
  && rm -rf /usr/local/man \
  && cp -rf cmake-3.13.3-Linux-x86_64/* /usr/local/ \
  && curl -SL http://leizaki.com/nextcloud/index.php/s/mP3KsOOTRTGWl8j/download | tar xvz -C .

#CMD [ "" ]
