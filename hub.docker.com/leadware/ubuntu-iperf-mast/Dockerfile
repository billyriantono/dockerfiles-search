# Leadware
#
# IPerf Mcast Dockerfile
# https://bitbucket.org/leadware/dockerfile-iperf-mcast
# https://jetune@bitbucket.org/leadware/dockerfile-iperf-mcast.git
# git@bitbucket.org:leadware/dockerfile-iperf-mcast.git
#

# Pull base image.
FROM ubuntu:18.04

# Maintainer
MAINTAINER Jean-Jacques ETUNÈ NGI<jetune@leadware.net>

# Update apt repository, Install iperf.
RUN \
  apt-get update && \
  apt-get install -y iperf && \
  rm -rf /var/lib/apt/lists/*
    
# Add Entry point script file
ADD entrypoint.sh /leadware-entrypoint.sh

# Give wright to all sh file
RUN chmod 755 /leadware-entrypoint.sh

# Command
CMD ["/leadware-entrypoint.sh"]
