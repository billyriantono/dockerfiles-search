#AlertManager Config Store Dockerfile
FROM alpine
LABEL maintainer "Pavithra K C"

RUN apk --no-cache add curl

RUN mkdir -p /etc/alertmanager/

ADD config.yml /etc/alertmanager/config.yml

RUN chmod 766 /etc/alertmanager/config.yml

ADD docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod o+x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/bin/sh"]
