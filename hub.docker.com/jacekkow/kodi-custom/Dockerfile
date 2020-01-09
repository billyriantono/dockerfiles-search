FROM jacekkow/kodi

RUN echo "Europe/Warsaw" > /etc/timezone \
	&& rm -f /etc/localtime \
	&& dpkg-reconfigure -f noninteractive tzdata \
	&& apt-get -y update \
	&& apt-get -y install python-pycryptodome libnss3 \
	&& apt-get -y clean
