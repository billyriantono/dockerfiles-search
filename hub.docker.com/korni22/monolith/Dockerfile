FROM alpine AS build
RUN apk update &&\
    apk add git build-base openssl-dev \
    rust cargo
ENV RUSTFLAGS="-C target-feature=+crt-static"
WORKDIR /root/
RUN git clone https://github.com/Y2Z/monolith.git
RUN cd monolith && cargo build --target x86_64-alpine-linux-musl --release

FROM scratch
COPY --from=0 /root/monolith/target/x86_64-alpine-linux-musl/release/monolith /root/monolith
CMD ["/root/monolith"]
