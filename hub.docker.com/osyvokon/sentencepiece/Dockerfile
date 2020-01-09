FROM alpine:latest

RUN apk add --no-cache cmake g++ protobuf protobuf-dev make


WORKDIR /build
RUN wget https://github.com/google/sentencepiece/archive/v0.1.84.tar.gz && \
    tar xzf v0.1.84.tar.gz && cd sentencepiece-0.1.84 && mkdir build && cd build && \
    cmake .. && make -j2 && make install && rm -rf /build

WORKDIR /home

FROM alpine:latest
RUN apk add --no-cache libgcc libstdc++
COPY --from=0 /usr/local/lib/libsentencepiece*.so.0 /usr/local/lib/
COPY --from=0 /usr/local/bin/spm_* /usr/local/bin/
