FROM mcuadros/ofelia AS ofelia
FROM ubuntu

RUN apt-get update && apt-get install -y \
    ca-certificates \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

COPY --from=ofelia /usr/bin/ofelia /usr/bin/ofelia
COPY ofelia/config.ini /etc/ofelia/
COPY bin/append-slack-webhook.sh /usr/bin/

ENTRYPOINT ["/usr/bin/append-slack-webhook.sh"]

CMD ["/usr/bin/ofelia", "daemon", "--config", "/etc/ofelia/config.ini"]
