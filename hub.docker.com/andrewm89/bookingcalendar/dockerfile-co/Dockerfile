FROM alpine:latest

MAINTAINER Andre van Schalkwyk "andre@hebe.ch"

# Install
RUN apk update && apk add supervisor net-tools curl bind-tools vim

# supervisor
COPY supervisord.conf /etc/supervisord.conf

VOLUME /etc/supervisor/conf.d/

# start stuff
CMD ["supervisord", "-n"]
