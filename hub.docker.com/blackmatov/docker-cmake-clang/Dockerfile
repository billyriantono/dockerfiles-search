FROM blackmatov/docker-cmake-gcc

ENV CLANG_VERSION 6.0

RUN set -ex; \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -; \
    echo "deb http://apt.llvm.org/stretch/ llvm-toolchain-stretch-${CLANG_VERSION} main" > /etc/apt/sources.list.d/llvm.list;

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends clang-${CLANG_VERSION}; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*;

RUN set -ex; \
    update-alternatives --install /usr/bin/clang clang /usr/bin/clang-${CLANG_VERSION} 999; \
    update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-${CLANG_VERSION} 999

ENV CC clang
ENV CXX clang++