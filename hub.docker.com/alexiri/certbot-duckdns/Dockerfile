FROM certbot/certbot

RUN apk add --no-cache curl
COPY authenticator.sh cleanup.sh src/certbot-duckdns/
COPY entry.sh .

ENTRYPOINT [ "/opt/certbot/entry.sh" ]
