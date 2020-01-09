FROM debian:stretch

RUN apt-get update \
    && apt-get install -y curl lksctp-tools
RUN cd /tmp \
    && curl -sL http://emqtt.com/downloads/2316/debian9-deb -o emqttd.deb \
    && dpkg -i emqttd.deb

ADD emq.conf /etc/emqttd/emq.conf
ADD docker-entrypoint.sh /entrypoint.sh

EXPOSE 1883 8883 8083 8084 18083 4369 6000-6999

CMD ["/bin/bash", "-c", "/entrypoint.sh"]