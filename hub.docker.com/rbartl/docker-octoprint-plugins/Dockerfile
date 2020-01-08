FROM rbartl/docker-octoprint
MAINTAINER Robert Bartl <robert@edv-bartl.>

RUN set -xe \
	&& cd /tmp/ \
	&& echo "Install OctoPrint plugins" \
	&& pip install https://github.com/foosel/OctoPrint-DisplayZ/archive/master.zip \
        && pip install https://github.com/dattas/OctoPrint-DetailedProgress/archive/master.zip \
        && pip install https://github.com/OctoPrint/OctoPrint-MQTT/archive/master.zip \
        && pip install https://github.com/BillyBlaze/OctoPrint-TouchUI/archive/master.zip \
        && pip install https://github.com/OctoPrint/OctoPrint-DisplayProgress/archive/master.zip \
        && pip install https://github.com/imrahil/OctoPrint-NavbarTemp/archive/master.zip


