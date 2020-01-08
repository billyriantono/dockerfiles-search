FROM		debian:jessie
MAINTAINER	Victor M. Varela <v.varela@neartechnologies.com>

ENV		SYNCTHING_VERSION	v0.11.25

RUN		apt-get update -qq \
	&&	apt-get install -y --no-install-recommends tar wget \
	&&	wget -O /tmp/syncthing.tar.gz --no-check-certificate \
		"https://github.com/syncthing/syncthing/releases/download/$SYNCTHING_VERSION/syncthing-linux-amd64-$SYNCTHING_VERSION.tar.gz" \
	&&	tar xvzf /tmp/syncthing.tar.gz -C /tmp \
	&&	mv /tmp/syncthing-linux-amd64-$SYNCTHING_VERSION/syncthing /usr/local/bin \
	&&	mkdir -p /config \
	&&	apt-get remove -y wget \
	&&      rm -rf /var/lib/apt/lists/* /tmp/*

EXPOSE		22000 8080

CMD		["syncthing","--home=/config","--gui-address=0.0.0.0:8080"]

