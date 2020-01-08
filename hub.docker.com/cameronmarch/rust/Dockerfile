FROM alpine:latest

RUN apk update \
 && apk upgrade \
 && apk add libgcc \
 && apk add curl \
 && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > rustup-init.sh \
 && sh rustup-init.sh -y \
 && export PATH=$HOME/.cargo/bin:$PATH