# Base OS
FROM incendonet/centos7-mono
MAINTAINER info@incendonet.com

# Env setup
ENV HOME /root
WORKDIR ~/

# Get updates and build deps
RUN \
	yum -y update && \
	yum install -y httpd

# Mono install
RUN \
	yum -y install mono-web xsp apache2-mod_mono

