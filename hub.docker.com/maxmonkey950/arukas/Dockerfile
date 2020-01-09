FROM ilemonrain/ubuntu-sshd

ENV CONFIG_PORT=""
ENV CONFIG_UUID=""

RUN cd /tmp && \
    wget https://install.direct/go.sh && \
    bash go.sh

ADD entrypoint.sh /entrypoint.sh
ADD config.json /etc/v2ray/config.json

RUN chmod +x /entrypoint.sh 

ENTRYPOINT  /entrypoint.sh

EXPOSE 22
EXPOSE 54188
