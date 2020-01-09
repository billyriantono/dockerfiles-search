FROM jpetazzo/dind:latest
MAINTAINER fernando@tutum.co

ENV DOCKER_VERSION 1.5.0

RUN	echo deb http://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list && \
	  apt-key adv --keyserver pgp.mit.edu --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9

RUN apt-get update && apt-get install -y curl lxc-docker-$DOCKER_VERSION && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN curl -L https://github.com/docker/compose/releases/download/1.1.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose

ADD build.sh /

CMD ["/build.sh"]
