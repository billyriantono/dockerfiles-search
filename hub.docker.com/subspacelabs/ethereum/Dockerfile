FROM subspacelabs/ubuntu:arm32v7

ENV \
    GETH_RELEASE=1.8.22-7fa3509e \
    GETH_ARCH=arm7 \
    GETH_MD5=cca76260ae19c19f0754c6a97b1bfc32

COPY docker/build.sh /build.sh
COPY docker/entrypoint.sh /entrypoint.sh

RUN ["/build.sh"]

EXPOSE 8545 8546

ENTRYPOINT ["/entrypoint.sh"]
