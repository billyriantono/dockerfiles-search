FROM debian:jessie

RUN apt-get update && \
	apt-get install -y software-properties-common apt-transport-https && \
	add-apt-repository "deb https://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" && \
	apt-get update && \
	apt-get install --force-yes -y postgresql-9.6

