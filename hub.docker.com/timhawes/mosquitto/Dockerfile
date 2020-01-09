FROM ubuntu:xenial

RUN apt-get update \
	&& apt-get install -y --no-install-recommends mosquitto \
	&& rm -r /var/lib/apt/lists/*
COPY mosquitto.conf /etc/mosquitto/mosquitto.conf

VOLUME /var/lib/mosquitto
CMD mosquitto -c /etc/mosquitto/mosquitto.conf
EXPOSE 1883
