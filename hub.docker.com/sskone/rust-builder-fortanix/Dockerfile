FROM ubuntu:xenial

# common packages
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    ca-certificates curl file \
    build-essential \
    gcc gcc-multilib clang libclang-dev cmake\
    apt-transport-https ca-certificates pkg-config \
    libssl-dev gnupg2 protobuf-compiler wget \
    autoconf automake autotools-dev libtool xutils-dev \
    software-properties-common && \
    rm -rf /var/lib/apt/lists/*



ENV SSL_VERSION=1.0.2q

RUN curl https://www.openssl.org/source/openssl-$SSL_VERSION.tar.gz -O && \
    tar -xzf openssl-$SSL_VERSION.tar.gz && \
    cd openssl-$SSL_VERSION && ./config shared && make depend && make install && \
    cd .. && rm -rf openssl-$SSL_VERSION*

#ENV OPENSSL_LIB_DIR=/usr/local/ssl/lib \
#    OPENSSL_INCLUDE_DIR=/usr/local/ssl/include \
#    OPENSSL_STATIC=1


# install toolchain
RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain nightly -y

ENV PATH=/root/.cargo/bin:$PATH
RUN add-apt-repository ppa:openjdk-r/ppa
RUN echo "deb https://download.fortanix.com/linux/apt xenial main" | tee -a /etc/apt/sources.list.d/fortanix.list >/dev/null
RUN curl -sSL "https://download.fortanix.com/linux/apt/fortanix.gpg" | apt-key add -
RUN apt-get -y update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install intel-sgx-dkms openjdk-11-jdk
RUN rustup target add x86_64-fortanix-unknown-sgx --toolchain nightly
RUN cargo install fortanix-sgx-tools sgxs-tools


#Set up volumes for source code
RUN mkdir /source
VOLUME ["/source"]

RUN mkdir /source/target
VOLUME ["/source/target"]

WORKDIR /source
