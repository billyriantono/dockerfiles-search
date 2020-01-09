FROM alpine:latest

MAINTAINER aussieade

COPY docker-start.sh /docker-start.sh
RUN apk update && apk add openvpn && chmod 755 /docker-start.sh

EXPOSE 1194
CMD ["/docker-start.sh"]
