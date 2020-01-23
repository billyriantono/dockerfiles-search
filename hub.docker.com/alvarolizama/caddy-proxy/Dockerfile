FROM alpine:edge
MAINTAINER Alvaro Lizama Molina <hola@alvarolizama.net>
RUN apk --no-cache add -U musl musl-dev caddy
EXPOSE 8000
CMD caddy -port 8000 "basicauth / $USER $PASS" "proxy / $HOST"
