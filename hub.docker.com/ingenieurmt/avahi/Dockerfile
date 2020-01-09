FROM alpine:latest
RUN apk add --update --no-cache avahi augeas

COPY entrypoint.sh /opt/
RUN chmod +x /opt/entrypoint.sh

ENTRYPOINT ["/opt/entrypoint.sh"]

MAINTAINER ingenieurmt <matthew@thompsons.id.au>
