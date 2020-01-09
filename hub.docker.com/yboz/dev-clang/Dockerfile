FROM yboz/graphical:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && apt-get install -y \
    build-essential \
    clang-6.0 \
    libc++-dev && \
    update-alternatives --install /usr/bin/cc cc /usr/bin/clang-6.0 100 && \
    update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 100 && \
    update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++-6.0 100 && \
    update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 100

USER dev
WORKDIR /home/dev
