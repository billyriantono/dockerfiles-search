FROM alpine:3.8

ENV VERSION 0.6.0

RUN apk --update add \
   bash \
   curl \
   git \
   g++ \
   make \
   openssh \
   openssl \
   openssl-dev \
   && rm -rf /var/cache/apk/*

RUN curl -L https://github.com/AGWA/git-crypt/archive/$VERSION.tar.gz | tar zxv -C /var/tmp && \
  cd /var/tmp/git-crypt-$VERSION && \
  make && \
  make install PREFIX=/usr/local && \
  rm -rf /var/tmp/git-crypt-$VERSION

COPY "entrypoint.sh" "/entrypoint.sh"
ENTRYPOINT ["/entrypoint.sh"]
