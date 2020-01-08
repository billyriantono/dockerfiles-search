FROM rust
WORKDIR /app
VOLUME ["/app"]
RUN rustup target add armv7-unknown-linux-gnueabihf
RUN apt-get update && apt-get install -y g++-arm-linux-gnueabihf libc6-dev-armhf-cross
RUN mkdir -p /.cargo && echo '[target.armv7-unknown-linux-gnueabihf]\n\
linker = "arm-linux-gnueabihf-gcc"\n\
ar = "/linux-runner armv7"' >> /.cargo/config