FROM alpine:latest

WORKDIR /root

RUN apk add --no-cache openssl

COPY entrypoint.sh .
RUN chmod +x entrypoint.sh

ENTRYPOINT ["./entrypoint.sh"]
