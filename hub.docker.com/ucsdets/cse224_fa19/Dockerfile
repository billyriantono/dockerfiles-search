ARG BASE_CONTAINER=ubuntu:18.04
FROM $BASE_CONTAINER

LABEL maintainer="UC San Diego ITS/ETS <servicedesk@ucsd.edu>"

USER root

######################################
# basic linux commands
# note that 'screen' requires additional help
# to function within a 'kubectl exec' terminal environment
RUN apt-get update && apt-get -qq install -y \
        	curl \
        	rsync \
        	unzip \
        	less nano \
		vim \
        	openssh-client \
		cmake \
		tmux \
		screen \
		gnupg \
        	wget \
		&& \
	chmod g-s /usr/bin/screen && \
	chmod 1777 /var/run/screen && \
	apt-get clean

# Install CSE224 requested packages
RUN apt-get update && apt-get -qq install -y \
		emacs-nox \
		build-essential \
		git \
		openjdk-8-jdk \
		libxmlrpc-c++8-dev \
		libxmlrpc-c++8v5 \
		libxmlrpc-core-c3 \
		libxmlrpc-core-c3-dev \
		libxmlrpc3-client-java \
		libxmlrpc3-common-java \
		libxmlrpc3-java-doc \
		libxmlrpc3-server-java \
		libcurlpp-dev \
		&& \
	apt-get clean

# Install nonprivileged test user 
RUN useradd -m -u 1000 testacct
USER 1000:1000

# Assuming container is built with:
#
#     docker build -t cse224_fa19:latest .
#
# you may launch an environment representative of student cluster via:
#
#     docker run -i -t -w /home/testacct cse224_fa19:latest /bin/bash -l
#

