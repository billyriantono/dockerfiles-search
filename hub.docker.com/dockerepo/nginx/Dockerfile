
FROM alpine:3.4

RUN apk add --update nginx
RUN rm -rf /var/cache/apk/* && rm -rf /tmp/*

RUN adduser -D -g '' -G www-data www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443