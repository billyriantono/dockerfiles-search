# Multistage docker build, requires docker 17.05

# builder stage
FROM rust:slim as builder

RUN set -ex && \
    apt-get update && \
    apt-get --no-install-recommends --yes install \
        cmake \
        clang \
        git \
        libssl-dev \
        pkg-config


RUN git clone https://github.com/vault713/wallet713 && \
    cd wallet713 && \
    cargo build --release
	
# runtime stage	
FROM debian:stretch-slim

RUN set -ex && \
    apt-get update	&& \
    apt-get --no-install-recommends --yes install \
		libssl-dev \
        pkg-config \
		apt-transport-https \
		ca-certificates
	
COPY --from=builder /wallet713/target/release/wallet713 /bin/wallet713

ENTRYPOINT ["/bin/wallet713"]

