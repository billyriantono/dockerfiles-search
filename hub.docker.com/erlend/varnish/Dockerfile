FROM alpine:3.4

RUN apk add --no-cache varnish

COPY entrypoint.sh /

CMD ["echo", "Varnish is unconfigured. Please see the README file"]
ENTRYPOINT ["/entrypoint.sh"]
