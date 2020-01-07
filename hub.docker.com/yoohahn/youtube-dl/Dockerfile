FROM alpine:edge
LABEL maintainer="yoohahn"

RUN set -xe \
  && apk add --no-cache \
    ca-certificates \
    ffmpeg \
    openssl \
    python3 \
  && pip3 install --upgrade pip \
  && pip3 install youtube-dl

WORKDIR /temp

ENTRYPOINT ["youtube-dl"]
CMD ["--help"]
