FROM alpine:latest

COPY ./entrypoint.sh /usr/bin/entrypoint.sh

RUN apk update && \
    apk add curl jq && \
    curl https://raw.githubusercontent.com/YadominJinta/DDNS-Helper/master/ddns-helper \
    -o /usr/bin/ddns-helper && \
    chmod +x /usr/bin/ddns-helper && \
    chmod +x /usr/bin/entrypoint.sh && \
    mkdir /etc/ddns.d 

ENTRYPOINT [ "entrypoint.sh" ]