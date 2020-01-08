# https://resin.io/blog/building-arm-containers-on-any-x86-machine-even-dockerhub/
FROM resin/armv7hf-debian-qemu

RUN ["cross-build-start"]

# http://phantomjs.org/build.html

RUN apt-get update && apt-get install -y git build-essential g++ flex bison gperf ruby perl \
      libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
      libpng-dev libjpeg-dev python libx11-dev libxext-dev

RUN git clone git://github.com/ariya/phantomjs.git

WORKDIR phantomjs/

RUN git checkout 2.1.1 && \
      git submodule init && \
      git submodule update

RUN python build.py

RUN ["cross-build-end"]
