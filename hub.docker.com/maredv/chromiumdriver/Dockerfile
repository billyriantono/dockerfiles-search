FROM ubuntu:16.04

# Update & upgrade system
RUN apt-get update && \
	apt-get upgrade -yq

# Install international fonts
RUN apt-get install -yq fonts-arphic-ukai fonts-arphic-uming fonts-ipafont-mincho fonts-ipafont-gothic fonts-unfonts-core

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    apt-get clean

RUN apt-get install -y chromium-chromedriver

# Installation cleanup
RUN apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Create data directory
RUN mkdir /data
WORKDIR /data

# Add chrome user
RUN addgroup chrome && \
	useradd -m -g chrome chrome
USER chrome

