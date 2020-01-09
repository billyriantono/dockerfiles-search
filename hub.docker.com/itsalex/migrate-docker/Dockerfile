FROM frolvlad/alpine-glibc as downloader

ENV VERSION 3.2.0
ENV DOWNLOAD_URL https://github.com/golang-migrate/migrate/releases/download/v$VERSION/migrate.linux-amd64.tar.gz

RUN apk add --no-cache ca-certificates openssl

RUN set -xe \
    && wget $DOWNLOAD_URL \
    && tar xvfz migrate.linux-amd64.tar.gz -C /tmp

FROM frolvlad/alpine-glibc

COPY --from=downloader /tmp/migrate.linux-amd64 /migrate
RUN chmod u+x /migrate

ENTRYPOINT ["/migrate"]
CMD ["--help"]
