FROM alpine:latest
MAINTAINER Andrei Manea <andrei@cloudhero.io>

ADD /bin/docker /usr/bin/docker
RUN apk update && apk add curl git nano

ADD docker-entrypoint.sh /entrypoint.sh
RUN chmod u+x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

