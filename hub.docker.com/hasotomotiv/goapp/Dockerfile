FROM alpine:latest
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>
# Upgrade
RUN apk update
RUN apk upgrade
RUN apk add ca-certificates && update-ca-certificates
# Change TimeZone
RUN apk add --update tzdata
RUN cp /usr/share/zoneinfo/Europe/Istanbul /etc/localtime
RUN echo "Europe/Istanbul" >  /etc/timezone
RUN apk del tzdata

ENV APPNAME "goapp"

VOLUME /srv
COPY srv /srv
COPY bin /bin

EXPOSE 80
ENTRYPOINT ["/bin/entrypoint.sh"]