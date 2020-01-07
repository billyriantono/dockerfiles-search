FROM alpine:3.5

ARG VERSION="v1.0.1"

WORKDIR /usr/local/src

RUN apk --no-cache add libpng-dev g++
RUN apk --no-cache \
        --virtual build-essential \
          add \
            git \
            make && \
    git clone https://github.com/google/guetzli.git \
      --branch "${VERSION}" \
      --depth 1 && \
    cd guetzli && make && \
    cp bin/Release/guetzli /usr/local/bin && \
    cd .. && rm -rf guetzli && \
    apk del build-essential && \
    adduser -D -s /bin/sh guetzli

USER guetzli
WORKDIR /home/guetzli

ENTRYPOINT ["guetzli"]