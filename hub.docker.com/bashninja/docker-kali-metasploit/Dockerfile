# Docker container with metasploit.
#
# Use Kali Linux base image (2.0)
FROM bashninja/docker-kali
MAINTAINER bashNinja <>

ENV DEBIAN_FRONTEND noninteractive

# Install metasploit
RUN apt-get -y update ; apt-get -y --force-yes install ruby metasploit-framework

# Attach this container to stdin when running, like this:
CMD /bin/bash
