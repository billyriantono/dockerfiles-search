FROM ubuntu
RUN apt-get update && apt-get install -y curl build-essential
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain=nightly
ENV USER=root
ENV PATH=/root/.cargo/bin:$PATH
