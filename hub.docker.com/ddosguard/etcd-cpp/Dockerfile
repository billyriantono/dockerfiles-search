FROM buildpack-deps:stretch AS builder

ENV PATH /usr/local/bin:$PATH
ENV LANG C.UTF-8

RUN set -ex \
    && apt-get update -qq \
    && apt-get install -y --no-install-recommends \
        libboost-all-dev \
        libcpprest-dev    \
        cmake              \
        gcc                 \
        catch                \
        golang                \
        git                    \
        checkinstall            \
    && mkdir /{export,app} \
    && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*

WORKDIR /app

RUN set -ex \
    && git clone --recursive https://github.com/grpc/grpc.git || true \
    && cd grpc \
    && make -j4 \
    && make install \
    && cd ../grpc/third_party/protobuf/ \
    && make install \
    && rm -fr /tmp/* /var/tmp/* /app/*


ARG PKGNAME=etcd-lib
ARG PKGVERSION=1.0

RUN set -ex \ 
    && mkdir /export \
    && git clone --recursive https://github.com/nokia/etcd-cpp-apiv3 || true \
    && cd etcd-cpp-apiv3/proto \
    && protoc -I . --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` ./rpc.proto \
    && protoc -I . --cpp_out=. ./*.proto \
    && cd .. \
    && mkdir build || true \
    && cd build \
    && cmake .. \
    && make -j4 \
    && checkinstall -Dy \
       --pkgname=${PKGNAME} \
       --install=no \
       --pkggroup=library \
       --pkgversion=${PKGVERSION} \
       -A amd64 \
       --maintainer=devops@ddos-guard.net \
       --pakdir=/app \
       --nodoc \
       --backup=no \
    && cd /app \
    && FILE=$(ls|grep deb) \
    && cp /app/$FILE /export\
    && rm -fr /tmp/* /var/tmp/*


FROM alpine
COPY --from=builder /export/ /app/
