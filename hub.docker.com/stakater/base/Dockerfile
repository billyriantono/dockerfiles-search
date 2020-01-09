############################################################
# Base Docker Image
############################################################

# From & maintainer
FROM 			phusion/baseimage:0.9.16
MAINTAINER 		Rasheed Amir <rasheed@aurorasolutions.io>

# Set TERM environment variable
ENV       TERM xterm
# Make sure the package repository is up to date
RUN 			echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN 			apt-get -y update

# Install python-software-properties (so you can do add-apt-repository)
RUN 			DEBIAN_FRONTEND=noninteractive apt-get install -y python-software-properties


# Install utilities
RUN 			apt-get -y install sudo nano git sudo zip bzip2 fontconfig wget


# Configure users
RUN 			echo 'root:stakater' |chpasswd
RUN 			groupadd stakater && useradd stakater -s /bin/bash -m -g stakater -G stakater && adduser stakater sudo
RUN 			echo 'stakater:stakater' |chpasswd
RUN 			cd /home && chown -R stakater:stakater /home/stakater


# Expose the working directory
VOLUME 			["/home/stakater"]
#####
# Phusion: Clean up APT when done.
#####
RUN 			apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Use baseimage-docker's init system.
# To run any custom scripts or daemons, please follow instructions:
# https://github.com/phusion/baseimage-docker#adding_additional_daemons
# https://github.com/phusion/baseimage-docker#running_startup_scripts
