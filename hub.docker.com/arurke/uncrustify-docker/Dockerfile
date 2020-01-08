FROM alpine:latest

RUN apk upgrade --update && \
    apk add --no-cache make bash build-base cmake python3 git

RUN mkdir -p /usr/src && cd /usr/src/ && \
    git clone https://github.com/uncrustify/uncrustify.git && \
    cd uncrustify && \
    git checkout uncrustify-0.69.0 && \
    mkdir build && cd build && \
    cmake .. && \
    cmake --build . && \
    make install && \
    rm -rf /usr/src && \
    uncrustify --version
