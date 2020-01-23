from alpine:3.8
RUN  echo http://dl-cdn.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories ; apk update ;  apk add crystal  bash git  make gcc llvm5 llvm5-dev g++ openssl-dev libxml2-dev shards

RUN export LLVM_CONFIG=/usr/src
RUN git clone -b 0.27.0 https://github.com/crystal-lang/crystal.git; cd crystal;  make ; ln -s /crystal/bin/crystal /usr/local/bin/crystal
