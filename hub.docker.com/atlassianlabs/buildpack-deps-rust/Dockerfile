FROM buildpack-deps

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
ENV PATH /root/.cargo/bin:$PATH
RUN rustup default nightly
RUN cargo install rustfmt
