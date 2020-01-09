FROM debian:stretch-slim AS base
RUN apt-get update && apt-get install -y --no-install-recommends \
    libboost-all-dev \
    libbz2-dev \
    libmariadbclient-dev \
    libncurses-dev \
    libreadline-dev \
    libssl1.0-dev \
    mariadb-client \
    p7zip \
    && rm -rf /var/lib/apt/lists/*

FROM base AS build
RUN apt-get update && apt-get install -y --no-install-recommends \
    clang \
    cmake \
    g++ \
    gcc \
    git \
    make
RUN update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100
RUN update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang 100
RUN mkdir -p /TrinityCore/build
COPY . /TrinityCore
WORKDIR /TrinityCore/build
RUN cmake /TrinityCore -DCMAKE_INSTALL_PREFIX=/usr/local
RUN make -j $(nproc) install

FROM base
COPY --from=build /usr/local/ /usr/local/
COPY --from=build /TrinityCore/sql/ /usr/local/sql
