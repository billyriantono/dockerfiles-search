FROM armel/busybox:uclibc

MAINTAINER Guillaume Goussard <guillaume.goussard@gmail.com>

WORKDIR /go/src/app

ADD https://dl.minio.io/server/minio/release/linux-arm6vl/minio minio

EXPOSE 9000
ENTRYPOINT ["sh"]
CMD ["-c", "chmod +x minio && ./minio"]
VOLUME ["/export"]
