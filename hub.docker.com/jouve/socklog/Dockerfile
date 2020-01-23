FROM alpine:3.8

RUN apk add --no-cache socklog

EXPOSE 514/udp

CMD [ "socklog", "inet" ]

