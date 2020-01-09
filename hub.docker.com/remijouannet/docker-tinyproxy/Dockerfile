FROM alpine:3.3
MAINTAINER Rémi Jouannet remijouannet@gmail.com

WORKDIR /app

RUN apk update && apk upgrade
RUN apk add tinyproxy

COPY . /app/

RUN chmod a+r /app/tinyproxy.conf
RUN chmod u+x /app/run.sh

EXPOSE 8859:8859

CMD ["/app/run.sh"]
