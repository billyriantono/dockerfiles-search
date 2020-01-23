FROM library/ubuntu:vivid

RUN \
	apt-get update && \
	DEBIAN_FRONTEND=noninteractive \
		apt-get -y install openjdk-8-jre-headless \
	&& \
	apt-get autoremove && \
	apt-get autoclean && \
	apt-get clean
