FROM pingcap/pd

MAINTAINER Huang Rui <vowstar@gmail.com>

ADD ./start.sh /start.sh

ENV CLIENT_PORT=2379 \
    PEER_PORT=2380

ENTRYPOINT []

CMD ["/start.sh"]

VOLUME ["/var/pd"]

EXPOSE ${CLIENT_PORT} ${PEER_PORT}
