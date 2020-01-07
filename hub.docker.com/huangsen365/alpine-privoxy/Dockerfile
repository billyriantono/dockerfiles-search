FROM alpine:3.8

RUN apk add --no-cache privoxy

COPY ./config /etc/privoxy/config
EXPOSE 8080
CMD privoxy --no-daemon /etc/privoxy/config
