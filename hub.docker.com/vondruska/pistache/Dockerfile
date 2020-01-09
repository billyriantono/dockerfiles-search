FROM alpine:latest

WORKDIR /build
RUN apk update && \
    apk add g++ git cmake make && \
    git clone https://github.com/oktal/pistache.git . && \
    git submodule update --init && \
    mkdir build && \
    cd build && \
    cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release .. && \
    make && \
    make install