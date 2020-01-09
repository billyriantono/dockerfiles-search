FROM clux/muslrust:latest

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y clang libclang-dev && \
	rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src
RUN curl https://download.libsodium.org/libsodium/releases/libsodium-1.0.16.tar.gz | tar zx
WORKDIR /usr/src/libsodium-1.0.16
RUN ./configure --enable-shared=no
RUN make && make check && make install

WORKDIR /usr/src/garlichatd
COPY . .
RUN cd garlichatd && PKG_CONFIG_ALLOW_CROSS=1 SODIUM_LIB_DIR=/usr/local/lib \
	SODIUM_STATIC=static cargo build --release

FROM scratch
COPY --from=0 /usr/src/garlichatd/target/x86_64-unknown-linux-musl/release/garlichatd /garlichatd
CMD ["/garlichatd"]
