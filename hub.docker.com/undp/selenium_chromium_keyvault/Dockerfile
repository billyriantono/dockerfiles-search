#=======================
# Base image to be used
#=======================
FROM amd64/debian:stable-slim

#==============================================
# Maintainer Information & Project description
#==============================================
LABEL	maintainer="olivier.simah@undp.org" \
		description="Docker container for Selenium Testing with Chrome and access to Azure KeyVault"

#====================================================
# Create a selenium folder where the scripts will be
#====================================================
RUN mkdir -p /selenium

#========================================================
# Adding Debian official repo and installing needed apps
#========================================================
# First line to avoid a BUG while upgrading
RUN echo "deb http://ftp.debian.org/debian testing main" | tee --append /etc/apt/sources.list && \
	mkdir -p /usr/share/man/man1/ && touch /usr/share/man/man1/sh.distrib.1.gz && \
	apt update && \
	apt -y upgrade && \
	apt -y autoremove && \
	apt -y install python3 \
		python3-pip \
		chromium \
		libnss3-dev \
		unzip \
		curl \
		xvfb \
		wget \
		gnupg2
		
#======================================================
# Chrome Driver - USELESS AS IT IS INSTALLED FROM REPO
#======================================================
RUN CHROME_DRIVER_VERSION=`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE` && \
	wget -N https://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip -P /tmp && \
	unzip /tmp/chromedriver_linux64.zip -d /tmp && \
	rm /tmp/chromedriver_linux64.zip && \
	chmod +x /tmp/chromedriver && \
	mv -f /tmp/chromedriver /usr/local/bin/chromedriver

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
	apt-get update && \
	apt-get upgrade -y && \
	apt-get autoremove -y

#====================================
# Setting some environment variables
#====================================
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV appID="set_id"
ENV appKey="set_key"

WORKDIR /selenium
