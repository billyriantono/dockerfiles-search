FROM alpine:latest
LABEL maintainer="kosar@freedom.valor.ua"
LABEL vendor="1node"
LABEL lastUpdate="31-08-2019"
LABEL description="Squid alpine"
EXPOSE 3128
RUN apk update && apk upgrade
# set timezone
RUN apk add tzdata && cp /usr/share/zoneinfo/Europe/Kiev /etc/localtime && apk del tzdata
# install Squid
RUN apk add squid
CMD ["squid --foreground -Cd 1"]
