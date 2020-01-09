FROM ubuntu:16.04
LABEL maintainer "@twistify"
LABEL description "HomeAssistant with MQTT on Ubuntu"

# install python 3 and Mosquitto (from PPA to get latest version - Ubuntu packages a little old)
RUN apt-get update && \
    apt-get -y install build-essential libssl-dev python3 python3-pip python3-dev software-properties-common && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 install --upgrade pip && \
    pip3 install --upgrade virtualenv

# install Mosquitto MQTT Broker
RUN add-apt-repository -y ppa:mosquitto-dev/mosquitto-ppa && \
    apt-get update && \
    apt-get -y install mosquitto mosquitto-clients && \
    rm -rf /var/lib/apt/lists/*

# install Home Assistant, we need to change shell to bash from sh to succeed
SHELL ["/bin/bash", "-c"]
RUN adduser --system homeassistant && \
    usermod -G dialout -a homeassistant && \
    mkdir /homeassistant && \
    mkdir /homeassistant/config && \
    chown homeassistant /homeassistant &&\
    chown homeassistant /homeassistant/config &&\
    su -s /bin/bash homeassistant && \
    virtualenv -p python3 /homeassistant && \
    source /homeassistant/bin/activate && \
    pip3 install --upgrade homeassistant


COPY startup.sh /startup.sh
RUN chmod +x /startup.sh

VOLUME /homeassistant/config
EXPOSE 8123
EXPOSE 1883

ENTRYPOINT ["/startup.sh"]
