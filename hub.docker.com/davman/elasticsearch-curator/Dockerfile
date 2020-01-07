FROM alpine:latest
MAINTAINER David Manso <david.manso@epistolae.com>

RUN apk --no-cache add py-pip && pip install elasticsearch-curator

COPY entrypoint.sh /
RUN chmod 755 /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

WORKDIR /config

ENV INTERVAL=3600

USER nobody:nobody
