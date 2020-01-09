FROM alpine:latest
RUN apk add --update --no-cache smartmontools

COPY smartd.conf /etc/
COPY entrypoint.sh /opt/

RUN chmod +x /opt/entrypoint.sh

ENTRYPOINT ["/opt/entrypoint.sh", "-n", "--quit=never", "--attributelog=/var/log/smartd/"]
CMD ["--interval=10"]

MAINTAINER ingenieurmt <matthew@thompsons.id.au>
