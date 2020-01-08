FROM rust:1.33.0-slim-stretch

RUN apt-get update && \
    apt-get install -y build-essential curl git gnupg software-properties-common apt-transport-https && \
    apt-get clean && rm -rf /var/lib/apt/lists/* rm -rf /tmp/*

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys AA12E97F0881517F && \
    add-apt-repository 'deb https://static.redox-os.org/toolchain/apt /' && \
    apt-get update && apt-get install -y x86-64-unknown-redox-gcc && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

ENV CC="x86_64-unknown-redox-gcc"
