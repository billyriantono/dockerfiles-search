FROM prasad7676/base-ubuntu

LABEL maintainer="IntHunter(Prasad Patel)"

RUN apt-get update && \
    apt-get install -y mosquitto mosquitto-clients && \
    mkdir Config
COPY /root /

COPY /Config /Config

EXPOSE 1883/tcp 9001/tcp

VOLUME /etc/mosquitto /var/log/mosquitto/ /var/lib/mosquitto/
