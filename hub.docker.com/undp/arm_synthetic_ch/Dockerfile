#=======================
# Base image to be used
#=======================
FROM resin/armv7hf-debian-qemu

RUN [ "cross-build-start" ]

#==============================================
# Maintainer Information & Project description
#==============================================
LABEL	maintainer="osimood@gmail.com" \
			description="Docker container for Selenium Testing with Chromium"

#====================================================
# Create a selenium folder where the scripts will be
#====================================================
ENV SELENIUM_DIR /selenium
RUN mkdir -p $SELENIUM_DIR

#============================================================
# Updating and installing the apps necessary for this script
#============================================================
RUN apt-get update && \
	apt-get install -y gnupg2 \
		curl \
		wget

#===============================================================
# Adding repositories in order to install all dependencies apps
#===============================================================
RUN echo "deb http://httpredir.debian.org/debian stretch main contrib non-free" | tee --append /etc/apt/sources.list && \
	echo "deb http://httpredir.debian.org/debian stretch-updates main contrib non-free" | tee --append /etc/apt/sources.list && \
	echo "deb http://httpredir.debian.org/debian stretch-backports main contrib non-free" | tee --append /etc/apt/sources.list && \
	echo "deb http://security.debian.org/ stretch/updates main contrib non-free" | tee --append /etc/apt/sources.list && \
	echo "deb http://ports.ubuntu.com/ bionic main restricted universe multiverse" | tee --append /etc/apt/sources.list && \
	echo "deb http://ports.ubuntu.com/ bionic-security main restricted universe multiverse" | tee --append /etc/apt/sources.list && \
	echo "deb http://ports.ubuntu.com/ bionic-updates main restricted universe multiverse" | tee --append /etc/apt/sources.list && \
	echo "deb http://ports.ubuntu.com/ bionic-backports main restricted universe multiverse" | tee --append /etc/apt/sources.list && \
	apt-key adv --no-tty --keyserver keyserver.ubuntu.com --recv-keys EF0F382A1A7B6500 && \
	apt-key adv --no-tty --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32


#============================
# Installing all needed apps
#============================
# First line to avoid a BUG while upgrading
RUN mkdir -p /usr/share/man/man1/ && touch /usr/share/man/man1/sh.distrib.1.gz && \
	apt-get update && \
	apt-get autoremove -y && \
	apt-get upgrade -y && \
	apt-get install -y python3 \
		python3-pip \
		xvfb \
		unzip \
		chromium \
		chromium-chromedriver \
		software-properties-common \
		unzip \
		xvfb

#=====================
# Python Modules used
#=====================
RUN pip3 install --upgrade pip setuptools
RUN pip3 install selenium
RUN pip3 install requests
RUN pip3 install selenium
RUN pip3 install PyVirtualDisplay
RUN pip3 install xvfbwrapper

#==========
# Clean up
#==========
RUN apt-get remove -y unzip \
	curl \
	wget && \
	apt-get autoremove -y

#====================================
# Setting some environment variables
#====================================
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

WORKDIR $SELENIUM_DIR

RUN [ "cross-build-end" ]
