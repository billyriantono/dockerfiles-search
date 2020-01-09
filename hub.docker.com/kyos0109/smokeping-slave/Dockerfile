FROM alpine:3.10

COPY ./tcpping /usr/bin/

COPY ./entrypoint.sh /entrypoint.sh

RUN apk add --no-cache smokeping tcptraceroute curl && \
    chmod 600 /etc/smokeping/smokeping_secrets && \
    chmod 755 /usr/bin/tcpping

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]

CMD ["/usr/bin/smokeping", "-h"]