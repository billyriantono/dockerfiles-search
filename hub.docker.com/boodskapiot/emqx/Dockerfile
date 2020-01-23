FROM boodskapiot/ubuntu:18.04.jdk13

MAINTAINER platform@boodskap.io

LABEL Remarks="EMQTTD preconfigured for Boodskap IoT Platform"

WORKDIR /

RUN wget --no-check-certificate  https://www.emqx.io/downloads/broker/v3.2.7/emqx-ubuntu18.04-v3.2.7.zip
RUN unzip emqx-ubuntu18.04-v3.2.7.zip
RUN mv emqx/* /root/
RUN rm -rf emqx
RUN echo "{emqx_auth_http, true}." >> /root/data/loaded_plugins

COPY etc/ /etc/
COPY root/ /root/
COPY start-emqtt.sh .

RUN chmod +x start-emqtt.sh

EXPOSE 1883 8083

CMD ["/start-emqtt.sh"]
