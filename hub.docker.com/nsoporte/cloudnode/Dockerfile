FROM		debian:buster


RUN			apt-get update; apt-get -y upgrade; \	
			apt-get -y install openvpn



COPY		files/ns-start /usr/bin/
COPY		files/ca.crt /etc/openvpn/
COPY		files/client.crt /etc/openvpn/
COPY		files/client.key /etc/openvpn/
COPY		files/cloudnode1.conf /etc/openvpn/
COPY		files/keypass /etc/openvpn/


RUN			chmod +x /usr/bin/ns-start; \
			mkdir /log


ENTRYPOINT [ "/usr/bin/ns-start" ]
