FROM ubuntu

RUN apt-get update && \
    apt-get install -y curl wget file git gcc

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

ENV PATH "$PATH:/root/.cargo/bin"

RUN rustup install 1.36.0
RUN rustup update

#ENV RUSTFMT_VERSION 0.3.1
#RUN wget https://github.com/rust-lang-nursery/rustfmt/archive/${RUSTFMT_VERSION}.tar.gz && \
#    tar xzf ${RUSTFMT_VERSION}.tar.gz && rm ${RUSTFMT_VERSION}.tar.gz && \
#    cd rustfmt-${RUSTFMT_VERSION} && \
#    $HOME/.cargo/bin/cargo install --path . && \
#    cd .. && rm -rf rustfmt-${RUSTFMT_VERSION}
