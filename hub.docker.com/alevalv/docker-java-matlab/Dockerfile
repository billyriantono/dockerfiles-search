FROM openjdk:8u141

MAINTAINER Alejandro Valdes

ADD matlab.txt /mcr-install/matlab.txt
#ADD MCR_R2016a_glnxa64_installer.zip /mcr-install/MCR_R2016a_glnxa64_installer.zip

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

RUN apt-get update && \
	apt-get install -y curl wget unzip xorg

# Install MatLab runtime
RUN \
	cd /mcr-install && \
	wget -nv http://de.mathworks.com/supportfiles/downloads/R2016a/deployment_files/R2016a/installers/glnxa64/MCR_R2016a_glnxa64_installer.zip && \
	unzip MCR_R2016a_glnxa64_installer.zip && \
	mkdir /opt/mcr && \
	./install -inputFile matlab.txt && \
	cd / && \
	rm -rf mcr-install

