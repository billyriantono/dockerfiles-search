#=======================
# Base image to be used
#=======================
FROM resin/armv7hf-debian-qemu

RUN [ "cross-build-start" ]

#==============================================
# Maintainer Information & Project description
#==============================================
LABEL	maintainer="osimood@gmail.com" \
	description="Docker container for Selenium Testing with Firefox"

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
		firefox \
		software-properties-common \
		unzip \
		xvfb

#=============
# GeckoDriver
#=============
ARG GECKODRIVER_VERSION=latest
RUN GK_VERSION=$(if [ ${GECKODRIVER_VERSION:-latest} = "latest" ]; then echo "0.23.0"; else echo $GECKODRIVER_VERSION; fi) \
	&& echo "Using GeckoDriver version: "$GK_VERSION \
	&& wget --no-verbose -O /tmp/geckodriver.tar.gz https://github.com/mozilla/geckodriver/releases/download/v$GK_VERSION/geckodriver-v$GK_VERSION-arm7hf.tar.gz \
	&& rm -rf /opt/geckodriver \
	&& tar -C /opt -zxf /tmp/geckodriver.tar.gz \
	&& rm /tmp/geckodriver.tar.gz \
	&& mv /opt/geckodriver /opt/geckodriver-$GK_VERSION \
	&& chmod 755 /opt/geckodriver-$GK_VERSION \
	&& ln -fs /opt/geckodriver-$GK_VERSION /usr/local/bin/geckodriver

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
	gnupg2 \
	wget && \
	apt autoremove -y

#====================================
# Setting some environment variables
#====================================
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

WORKDIR $SELENIUM_DIR

RUN [ "cross-build-end" ]
