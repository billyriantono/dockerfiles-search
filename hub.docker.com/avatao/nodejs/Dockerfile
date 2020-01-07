FROM avatao/ubuntu:16.04

RUN cd ~ \
	&& curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh \
	&& bash nodesource_setup.sh \
	&& apt-get update \
	&& apt-get install -qy \
		nodejs \
		mongodb
