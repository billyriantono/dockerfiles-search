FROM alpine:edge

RUN apk add --no-cache git ruby && \
  \
  apk add --no-cache --virtual .build-deps \
    g++ \
    make \
    ruby-dev \
    libffi-dev && \
  \
  gem install travis -v 1.8.10 --no-rdoc --no-ri && \
  \
  apk del .build-deps && \
  \
  adduser -D -g users dev && \
  su -c 'mkdir -p ~/.travis' - dev

USER dev
WORKDIR /home/dev

VOLUME ["/home/dev/.travis"]
ENTRYPOINT ["travis"]