FROM resin/armv7hf-debian:latest

RUN [ "cross-build-start" ] 

RUN apt-get update && apt-get install -y transmission-daemon

COPY settings.json /etc/transmission-daemon/settings.json
COPY transmission-daemon /etc/default/transmission-daemon

RUN touch /var/log/transmission.log

RUN [ "cross-build-end" ]  

VOLUME /var/lib/transmission-daemon/downloads /var/lib/transmission-daemon/Downloads

EXPOSE 9091

CMD service transmission-daemon start && tail -F /var/log/transmission.log
