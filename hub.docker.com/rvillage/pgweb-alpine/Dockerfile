FROM alpine:3.6
LABEL maintainer "rvillage <rvillage@gmail.com>"

ENV PGWEB_VERSION 0.9.7

RUN set -ex \
    && apk --update --upgrade add --no-cache --virtual .build_pgweb \
         ca-certificates \
         openssl-dev \
         unzip \
         wget \
    && wget https://github.com/sosedoff/pgweb/releases/download/v${PGWEB_VERSION}/pgweb_linux_amd64.zip \
    && unzip pgweb_linux_amd64.zip \
    && rm pgweb_linux_amd64.zip \
    && mv pgweb_linux_amd64 /bin/pgweb \
    && chmod +x /bin/pgweb \
    && apk del .build_pgweb

EXPOSE 8081

ENTRYPOINT ["pgweb", "-s", "--bind=0.0.0.0"]
