FROM alpine
LABEL maintainer="hello@olanmatt.com"

ARG VERSION=2019.9.28

RUN apk add --no-cache python3 \
    && pip3 install --no-cache-dir youtube-dl==$VERSION

WORKDIR /data

ENTRYPOINT [ "youtube-dl" ]
CMD [ "--help" ]