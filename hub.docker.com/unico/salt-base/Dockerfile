FROM ubuntu:latest
MAINTAINER Bryce Gibson "bryce.gibson@unico.com.au"

RUN echo "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main universe" > /etc/apt/sources.list ; \
    apt-get update && apt-get upgrade && apt-get install -y curl

ADD https://bootstrap.saltstack.com/ /tmp/install_salt.sh

# Don't start the daemons and install the master as well
RUN sh /tmp/install_salt.sh -X -M ; [ -f /usr/bin/salt-minion ] && [ -f /usr/bin/salt-master ] && echo 'salt-minion and salt-master appear to be installed. The "Failed to run install_ubuntu_check_services" error can likely be ignored as it is a limitation of the script for docker containers (see https://github.com/saltstack/salt-bootstrap/issues/394)'
