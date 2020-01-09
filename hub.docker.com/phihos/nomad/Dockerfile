FROM ubuntu:latest
MAINTAINER Philipp Hossner <philipp.hossner@posteo.de>

ENV NOMAD_VERSION 0.8.4

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -yq wget unzip
RUN wget https://releases.hashicorp.com/nomad/${NOMAD_VERSION}/nomad_${NOMAD_VERSION}_linux_amd64.zip -O /tmp/nomad.zip \
	&& unzip /tmp/nomad.zip -d /usr/bin/ \
	&& rm /tmp/nomad.zip \
	&& chmod +x /usr/bin/nomad

ENTRYPOINT ["/usr/bin/nomad"]


