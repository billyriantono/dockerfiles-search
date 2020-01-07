FROM selenium/node-chrome:latest

USER root
RUN apt-get -qqy update &&\
    apt-get install -y -q iptables &&\
    apt-get clean

COPY config.json /opt/selenium/config.json
COPY entrypoint.sh /opt/bin/entrypoint.sh

CMD ["/opt/bin/entrypoint.sh"]
