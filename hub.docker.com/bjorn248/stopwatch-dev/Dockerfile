FROM redis:alpine

LABEL maintainer "Yefta Sutanto <yefta@bitwyre.com>"

RUN apk add --no-cache \
        curl \
        bash
COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

EXPOSE 26379

ENTRYPOINT /docker-entrypoint.sh
