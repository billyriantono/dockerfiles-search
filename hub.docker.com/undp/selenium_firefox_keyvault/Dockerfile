#=======================
# Base image to be used
#=======================
FROM amd64/debian:stable-slim

#==============================================
# Maintainer Information & Project description
#==============================================
LABEL	maintainer="olivier.simah@undp.org" \
		description="Docker container for Selenium Testing with Firefox and access to Azure KeyVault"

#====================================================
# Create a selenium folder where the scripts will be
#====================================================
RUN mkdir -p /selenium

#========================================================
# Adding Debian official repo and installing needed apps
#========================================================
# First line to avoid a BUG while upgrading
RUN echo "deb http://ftp.debian.org/debian sid main" | tee --append /etc/apt/sources.list && \
	mkdir -p /usr/share/man/man1/ && touch /usr/share/man/man1/sh.distrib.1.gz && \
	apt update && \
	apt -y upgrade && \
	apt -y autoremove && \
	apt -y install python3 \
		python3-pip \
		firefox-esr \
		unzip \
		xvfb \
		curl \
		wget 
	
#=============
# GeckoDriver
#=============
ARG GECKODRIVER_VERSION=latest
RUN GK_VERSION=$(if [ ${GECKODRIVER_VERSION:-latest} = "latest" ]; then echo "0.24.0"; else echo $GECKODRIVER_VERSION; fi) \
	&& echo "Using GeckoDriver version: "$GK_VERSION \
	&& wget --no-verbose -O /tmp/geckodriver.tar.gz https://github.com/mozilla/geckodriver/releases/download/v$GK_VERSION/geckodriver-v$GK_VERSION-linux64.tar.gz \
	&& rm -rf /opt/geckodriver \
	&& tar -C /opt -zxf /tmp/geckodriver.tar.gz \
	&& rm /tmp/geckodriver.tar.gz \
	&& mv /opt/geckodriver /opt/geckodriver-$GK_VERSION \
	&& chmod 755 /opt/geckodriver-$GK_VERSION \
	&& ln -fs /opt/geckodriver-$GK_VERSION /usr/local/bin/geckodriver

#=====================
# Python Modules used
#=====================
RUN pip3 install --upgrade pip setuptools && \
	pip3 install selenium && \
	pip3 install requests && \
	pip3 install selenium && \
	pip3 install xvfbwrapper && \
	pip3 install azure && \
	pip3 install azure-keyvault

#==========
# Clean up
#==========
RUN apt-get remove -y unzip \
	curl \
	gnupg2 \
	wget && \
	apt update && \
	apt -y upgrade && \
	apt -y autoremove

#====================================
# Setting some environment variables
#====================================
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV appID="set_id"
ENV appKey="set_key"

WORKDIR /selenium
