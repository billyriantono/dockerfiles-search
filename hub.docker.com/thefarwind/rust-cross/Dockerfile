FROM rust:1.39.0-buster

RUN set -xe; \
	apt-get update; \
	apt-get install -y musl musl-tools; \
	rm -rf /var/lib/apt/lists/*; \
	rustup target add x86_64-unknown-linux-musl;

