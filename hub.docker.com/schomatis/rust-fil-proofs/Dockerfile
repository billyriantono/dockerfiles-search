# What does this Dockerfile do?
# =============================
#
# Incremental build of `rust-fil-proofs`.
# TODO: Expand on this.

FROM rust

# Get all the dependencies we can first
# -------------------------------------

# Copied from: github.com/filecoin-project/rust-fil-proofs/blob/master/Dockerfile-ci
RUN apt-get update && \
    apt-get install -y curl file gcc g++ git make openssh-client \
    autoconf automake cmake libtool libcurl4-openssl-dev libssl-dev \
    libelf-dev libdw-dev binutils-dev zlib1g-dev libiberty-dev wget \
    xz-utils pkg-config python clang

# Clone `rust-fil-proofs` repo
# ----------------------------

ENV HOME="/root"
# TODO: Is this needed? Isn't this already set? But does the Dockerfile
# have access to it?

ENV RUST_DIR=${HOME}/rust
RUN mkdir -p ${RUST_DIR}
WORKDIR ${RUST_DIR}
RUN git clone https://github.com/filecoin-project/rust-fil-proofs

# Build `master`
# --------------

ENV RUST_PROOFS_DIR=${RUST_DIR}/rust-fil-proofs
WORKDIR ${RUST_PROOFS_DIR}

RUN rustup install $(cat ${RUST_PROOFS_DIR}/rust-toolchain)
# Install toolchain first just to decouple some of the
# work that happens in the initial `build ` command.

ENV CARGO_INCREMENTAL=1
RUN cargo build --all --release -v -v --bins --examples --tests --benches
# Try to build everything we can *now*, the incremental build will
# let us rebuild only what we've modified later.
