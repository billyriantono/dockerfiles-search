FROM ubuntu:18.04

ENV PROTOC_ZIP=protoc-3.7.1-linux-x86_64.zip

WORKDIR /usr/src/app

RUN apt update
RUN apt upgrade -y
RUN apt install -y curl unzip gcc libldap-2.4-2 libldap-common libldap2-dev libpq-dev libpq5 pkg-config libssl-dev
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --profile minimal --default-toolchain stable
RUN PROTOC_ZIP=protoc-3.7.1-linux-x86_64.zip
RUN curl -OL https://github.com/protocolbuffers/protobuf/releases/download/v3.7.1/$PROTOC_ZIP
RUN unzip -o $PROTOC_ZIP -d /usr/local bin/protoc
RUN unzip -o $PROTOC_ZIP -d /usr/local 'include/*'
RUN rm -f $PROTOC_ZIP

ENV PATH="~/.cargo/bin:$PATH"

COPY . .
