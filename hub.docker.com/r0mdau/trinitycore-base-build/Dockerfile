FROM debian:stretch

LABEL name=r0mdau/trinitycore-base-build

RUN set -x && \
    apt-get update && \
    apt-get install -y \
        git \
        clang \
        cmake \
        make \
        gcc \
        g++ \
        libmariadbclient-dev \
        libssl-dev \
        libbz2-dev \
        libreadline-dev \
        libncurses-dev \
        libboost-all-dev \
        mariadb-server \
        p7zip \
        default-libmysqlclient-dev && \
    update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100 && \
    update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang 100 && \
    rm -rf /var/lib/apt/lists/*