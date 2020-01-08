FROM golang

# Package Installation
RUN apt-get update \
  && apt-get install -y \
  build-essential g++ flex bison gperf ruby perl \
  libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
  libpng-dev libjpeg-dev python libx11-dev libxext-dev \
  git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN cd / && git clone --recurse-submodules git://github.com/ariya/phantomjs.git \
  && cd /phantomjs \
  && git checkout -f 2.0.0 \
  && ./build.sh --jobs 1 --confirm --silent
