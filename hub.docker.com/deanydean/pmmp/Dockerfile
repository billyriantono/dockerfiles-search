#!/usr/bin/docker build
# Dockerfile for a PMMP server, from pmmp.io

# Based on Debian 9
FROM debian:9

# Add the files to the image
ADD ./scripts /opt/pmmp/scripts
ADD ./etc /opt/pmmp/etc

# Set up the system
RUN /opt/pmmp/scripts/init.sh

# Configure the system for pmmp
RUN /opt/pmmp/scripts/configure.sh

# Expose port 19132 for access (udp and tcp)
EXPOSE 19132/tcp
EXPOSE 19132/udp

# Start pmmp as the pocketmine user
ENTRYPOINT /opt/pmmp/scripts/start.sh
