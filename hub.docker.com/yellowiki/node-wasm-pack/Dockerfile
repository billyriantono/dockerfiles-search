FROM alpine:edge

RUN apk add cargo nodejs yarn openssl-dev
RUN apk add wabt --update-cache --repository http://dl.alpinelinux.org/alpine/edge/testing/
RUN cargo install wasm-pack

ENV PATH=/root/.cargo/bin:$PATH
