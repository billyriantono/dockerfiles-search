FROM alpine:edge

# Configure Go
ENV GOROOT /usr/lib/go
ENV GOPATH /go
ENV PATH /go/bin:$PATH

RUN mkdir -p ${GOPATH}/src ${GOPATH}/bin

RUN apk add --no-cache --virtual .build-deps autoconf automake libtool cmake git make g++ linux-headers go cargo rust pkgconfig  && \
  mkdir /tmp/build && cd /tmp/build && \
  git clone --recursive https://github.com/cloudflare/quiche && \
  cd quiche/deps/boringssl && \
  mkdir build && cd build && cmake -DCMAKE_POSITION_INDEPENDENT_CODE=on .. && make && cd .. && mkdir -p .openssl/lib && cp build/crypto/libcrypto.a build/ssl/libssl.a .openssl/lib && ln -s $PWD/include .openssl && \
  cd /tmp/build/quiche && \
  QUICHE_BSSL_PATH=/tmp/build/quiche/deps/boringssl cargo build --release --features pkg-config-meta && mkdir /usr/local/quiche && cp -R /tmp/build/quiche/target/release/* /usr/local/quiche && \
  cd /tmp/build && \
  git clone https://github.com/google/brotli && \
  cd brotli && \
  mkdir out && cd out && \
  ../configure-cmake && \
  make && make test && make install && \
  cd /tmp/build && \
  git clone https://github.com/tatsuhiro-t/nghttp2 && \
  cd nghttp2 && \
  autoreconf -i && automake && autoconf && \
  ./configure && \
  make && make install && \
  cd /tmp/build && \
  git clone https://github.com/curl/curl && \
  cd curl && \
  ./buildconf && \
  ./configure LDFLAGS="-Wl,-rpath,$PWD/../quiche/target/release" --with-ssl=$PWD/../quiche/deps/boringssl/.openssl --with-quiche=/usr/local/quiche --with-nghttp2=/usr/local --with-brotli --disable-shared && \
  make && make install && \
  rm -rf /tmp/build && \
  apk del .build-deps && \
  apk add ca-certificates libgcc

ENV LD_LIBRARY_PATH=/usr/local/openssl/lib:/usr/local/quiche

ENTRYPOINT ["curl"]
