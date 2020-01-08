FROM alpine

LABEL maintainer B. van Wetten <bas.van.wetten@gmail.com>

RUN apk --no-cache --update add curl && \
    rm -rf /var/lib/apt/lists/*

VOLUME /curl
WORKDIR /curl

ENTRYPOINT ["curl"]
CMD ["--help"]