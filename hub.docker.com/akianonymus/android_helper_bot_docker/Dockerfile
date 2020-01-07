FROM alpine:edge

# Install ca-certificates so that HTTPS works consistently
RUN apk add --no-cache ca-certificates

RUN apk add --no-cache --update \
      git \
      bash \
      nodejs \
      npm \
      build-base \
      jq

# Install python2
RUN apk add --no-cache python && \
    python -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools && \
    rm -r /root/.cache
    
# Build tdlib
RUN apk add --update alpine-sdk linux-headers git zlib-dev openssl-dev gperf php php-ctype cmake
WORKDIR /tmp/_build_tdlib/
RUN git clone https://github.com/Akianonymus/td.git -b test --depth 1 /tmp/_build_tdlib/
RUN rm -rf build && mkdir build
WORKDIR /tmp/_build_tdlib/build/
RUN export CXXFLAGS=""
RUN cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr/local ..
RUN cmake --build . --target prepare_cross_compiling
WORKDIR /tmp/_build_tdlib/
RUN php SplitSource.php
WORKDIR /tmp/_build_tdlib/build/
RUN cmake --build . --target install
WORKDIR /tmp/_build_tdlib/
RUN php SplitSource.php --undo
WORKDIR /tmp/_build_tdlib/
RUN ls -l /usr/local

# To handle not get uid/gid error while installing a npm package
RUN npm config set unsafe-perm true

RUN mkdir /bot
RUN chmod 777 /bot
WORKDIR /bot

