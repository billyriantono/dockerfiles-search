FROM alpine
LABEL maintainer="Narate Ketram <koonnarate@gmail.com>"
RUN apk add --update --no-cache netcat-openbsd
ADD ./json.http /json.http
ADD ./docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT /docker-entrypoint.sh
EXPOSE 80
