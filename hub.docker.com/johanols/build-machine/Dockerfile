FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
	clang-6.0 \
	cmake \
	libsdl2-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 999 \
 && update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 999 \
 && update-alternatives --install /usr/bin/cc cc /usr/bin/clang-6.0 999 \
 && update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++-6.0 999

ENV CC="clang" CXX="clang++"