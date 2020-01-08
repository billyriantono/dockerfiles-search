##
# Neo4j
##
# VERSION 	1.9-1
##

FROM 		ubuntu:14.04
MAINTAINER 	Robin W Larsson <robin@welovecloud.se>

##
# Set up environment
##
RUN echo 'Acquire::http { Proxy "http://naas.io:3142"; };' >> /etc/apt/apt.conf.d/01proxy

##
# Use non interactive mode for apt
##
ENV DEBIAN_FRONTEND noninteractive

##
# Upgrade system
##
RUN apt-get update
RUN apt-get -y dist-upgrade

##
# Install basic deps
##
RUN apt-get install -y wget

##
# Add Neo4j repos and install
##
RUN wget -O - http://debian.neo4j.org/neotechnology.gpg.key | apt-key add -
RUN echo 'deb http://debian.neo4j.org/repo stable/' > /etc/apt/sources.list.d/neo4j.list
RUN apt-get update
RUN apt-get install --no-install-recommends -y neo4j=1.9

##
# Make this thing fly
##
#RUN ulimit -n 65536
RUN sed -i 's/#org.neo4j.server.webserver.address=0.0.0.0/org.neo4j.server.webserver.address=0.0.0.0/g' /etc/neo4j/neo4j-server.properties

EXPOSE 7474
EXPOSE 7473

CMD  ["/bin/bash", "-c", "/var/lib/neo4j/bin/neo4j console"]
