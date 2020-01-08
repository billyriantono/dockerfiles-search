FROM ubuntu:18.04
LABEL maintainer="Mike Lubinets <public@mersinvald.me>"

# Update apt 
RUN apt update

# Install add-apt-repository
RUN apt-get install -y software-properties-common dirmngr apt-transport-https lsb-release ca-certificates

# Install deps
RUN apt-get install -y build-essential wget curl

# Add Wine PPA
RUN dpkg --add-architecture i386 \
    && wget -qO - https://dl.winehq.org/wine-builds/winehq.key | apt-key add - \
    && apt-add-repository -y 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main'

# Update apt again
RUN apt update

# Install wine
RUN apt-get install -y winehq-stable

# Install mingw64
RUN apt-get install -y mingw-w64

# Install Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
ENV PATH=/root/.cargo/bin:$PATH

# Install rust windows targets
RUN rustup target add x86_64-pc-windows-gnu
RUN rustup target add i686-pc-windows-gnu

RUN mkdir -p /root/.cargo
ADD config /root/.cargo
