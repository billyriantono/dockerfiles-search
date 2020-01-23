FROM ubuntu

WORKDIR /root/

RUN apt-get update && apt-get install wget -y
RUN wget http://dl.ubnt.com/unifi/5.0.6/unifi_sysvinit_all.deb

RUN dpkg -i unifi_sysvinit_all.deb || true
RUN apt-get -f install -y

EXPOSE 8080
EXPOSE 8443

ENTRYPOINT /etc/init.d/unifi start && tail -f /usr/lib/unifi/logs/server.log
