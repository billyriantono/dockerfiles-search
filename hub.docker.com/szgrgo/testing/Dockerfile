FROM alpine
#Only test
WORKDIR /opt

COPY docker-entrypoint.sh env.sh rabbit-config.sh ./

RUN chmod +x docker-entrypoint.sh

ENTRYPOINT ["/opt/docker-entrypoint.sh"]
