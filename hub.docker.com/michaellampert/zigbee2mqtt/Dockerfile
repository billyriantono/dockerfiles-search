FROM alpine

ARG source=https://github.com/Koenkk/zigbee2mqtt.git
ENV converter_source "https://github.com/Koenkk/zigbee-shepherd-converters.git"
ENV mqtt_server "mqtt://localhost"
ENV socat_ip ""
ENV socat_port 22
ENV serialdevice /dev/ttyACM0
ENV serialdevice_path /app/vusb/

COPY entrypoint.sh /

#Install
RUN chmod a+x /entrypoint.sh && \
	apk add --update --no-cache make gcc g++ python linux-headers udev nodejs npm git socat && \
	mkdir /app && \
	git clone $source /app && \
	cp /app/data/configuration.yaml /app && \
	cd /app && \
    npm install --unsafe-perm && \
    apk del make gcc g++ python linux-headers udev git
	
## Make SmartVISU "mountable" by end user
VOLUME /app/data

ENTRYPOINT ["/entrypoint.sh"]
