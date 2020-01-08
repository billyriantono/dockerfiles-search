FROM	jasonrivers/nagios

RUN	apt-get update; \
	apt-get -y upgrade


RUN	apt-get -y install python3-pip mariadb-client; \
	pip3 install requests; \
	pip3 install pysnmp

RUN	mkdir /opt/skin

ADD	files/skin.tgz  /opt

RUN	cd /opt/skin; \
	cp -rfv * /opt/nagios/share/
