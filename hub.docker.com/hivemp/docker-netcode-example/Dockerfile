FROM ubuntu:18.04 AS build
WORKDIR /build/
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y git wget unzip make libsodium23 libsodium-dev build-essential
RUN wget https://github.com/premake/premake-core/releases/download/v5.0.0-alpha12/premake-5.0.0-alpha12-linux.tar.gz
RUN tar -xvf premake-5.0.0-alpha12-linux.tar.gz
RUN git clone --branch v1.1 https://github.com/hach-que/netcode.io
WORKDIR /build/netcode.io/
RUN ../premake5 gmake
RUN make all

FROM ubuntu:18.04
RUN apt-get update && \
    apt-get install -y libsodium23 && \
    rm -rf /var/lib/apt/lists/*
COPY --from=build /build/netcode.io/bin/server /server
EXPOSE 40000/udp
ENTRYPOINT ["/server"]