FROM kartoza/geoserver:2.12.0

RUN apt-get update && apt-get install -y fontconfig

RUN wget -O /tmp/STIXBeta-ttf.zip https://sites.google.com/site/olegueret/STIXBeta-ttf.zip \
	&& unzip /tmp/STIXBeta-ttf.zip -d /tmp/stix \
	&& mv /tmp/stix/*.ttf /usr/share/fonts/truetype/ \
	&& rm -rf /tmp/stix

RUN apt-get install -y libmspack0 libfontenc1 libxfont1 xfonts-encodings cabextract xfonts-utils \
	&& wget -O /tmp/ttf-mscorefonts-installer_3.6_all.deb http://ftp.de.debian.org/debian/pool/contrib/m/msttcorefonts/ttf-mscorefonts-installer_3.6_all.deb \
	&& dpkg -i /tmp/ttf-mscorefonts-installer_3.6_all.deb \
	&& rm /tmp/ttf-mscorefonts-installer_3.6_all.deb

RUN fc-cache -f -s -v