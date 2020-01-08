FROM alpine:edge

RUN echo "ipv6" >> /etc/modules

RUN apk update && apk upgrade

RUN apk add --no-cache bash dpkg git
RUN apk add --no-cache clang clang-dev alpine-sdk gcc lld musl-dev
RUN apk add --no-cache cmake
RUN apk add --no-cache man man-pages

RUN ls -l /usr/bin/cc /usr/bin/c++ /usr/bin/clang /usr/bin/clang++ /usr/bin/ld

RUN ln -sf /usr/bin/clang /usr/bin/cc
RUN ln -sf /usr/bin/clang++ /usr/bin/c++
RUN ln -sf /usr/bin/lld /usr/bin/ld

RUN update-alternatives --install /usr/bin/cc cc /usr/bin/clang 10
RUN update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++ 10
RUN update-alternatives --install /usr/bin/ld ld /usr/bin/lld 10

RUN update-alternatives --auto cc
RUN update-alternatives --auto c++
RUN update-alternatives --auto ld

RUN update-alternatives --display cc
RUN update-alternatives --display c++
RUN update-alternatives --display ld

RUN ls -l /usr/bin/cc /usr/bin/c++ /usr/bin/ld

RUN cc --version
RUN c++ --version
RUN ld --version
