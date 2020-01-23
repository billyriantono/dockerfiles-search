FROM alpine:3.11
LABEL description="Commix docker container" \
      maintainer="Djerfy <djerfy@gmail.com>"

ENV VERSION=3.0-20191111

RUN apk -U add python wget && \
    wget https://github.com/commixproject/commix/archive/v${VERSION}.tar.gz -O commix.tar.gz && \
    tar xzf commix.tar.gz && \
    rm -f commix.tar.gz && \
    mv commix-${VERSION} /commix && \
    apk del wget

ENTRYPOINT ["/commix/commix.py"]

