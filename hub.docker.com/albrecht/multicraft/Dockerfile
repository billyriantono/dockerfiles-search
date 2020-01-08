FROM ubuntu:18.10
MAINTAINER Jonas Albrecht jonasalbrecht9@gmail.com

RUN adduser multicraft --gecos "" --no-create-home --disabled-password && passwd -d multicraft

ENV START=true \
	START_MODE=start

RUN apt-get update && apt-get install -y --no-install-recommends \
		default-jre \
		unzip \
		zip \
	&& rm -rf /var/lib/apt/lists/*

COPY ./src/multicraft /multicraft/
COPY ./startup.sh /root/


VOLUME ["/multicraft/"]
CMD ["/root/startup.sh"]