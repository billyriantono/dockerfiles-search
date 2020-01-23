FROM alpine:3.8
ENV VARNISH_MEMORY 100M
ENV VARNISH_START_CLI_FILE /etc/varnish/start.cli
ENV VARNISH_LISTEN_PORT 81

RUN apk update && apk upgrade && apk add varnish
ADD entrypoint.sh /entrypoint.sh

CMD ["/entrypoint.sh"]
