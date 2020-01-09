#AlertManager Dockerfile

FROM prom/alertmanager:v0.9.1
MAINTAINER Pavithra K C <Pavithra.KC@intlfcstone.com>

ADD docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod o+x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["-config.file=/etc/alertmanager/config.yml", \
             "-storage.path=/alertmanager"]
