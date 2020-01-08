FROM jawagang/docker-soutenances-base

MAINTAINER simodj_h@etna-alternance.net

RUN DEBIAN_FRONTEND=noninteractive apt-get update -y\
	&& wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg\
	&& sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ \
	&& wget -q https://packages.microsoft.com/config/debian/9/prod.list \
	&& sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list \
	&& sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg \
	&& sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list

RUN DEBIAN_FRONTEND=noninteractive apt-get update -y\
	&& apt-get install -y aspnetcore-runtime-2.1
	