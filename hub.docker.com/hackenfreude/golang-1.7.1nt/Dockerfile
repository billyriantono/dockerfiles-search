FROM ubuntu:trusty

LABEL maintainer="Nick Bascombe-Fox <nick.fox@ha247.co.uk>"

ENV DEBIAN_FRONTEND noninteractive

#######
# Application is installed with defaults. 
# ES data is in /usr/share/elasticsearch/data/
# Mount this volume in docker-compose.yaml
#######

# Install
RUN apt-get update
RUN apt-get -y install wget openjdk-7-jre curl
RUN  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.10.deb
RUN dpkg -i elasticsearch-0.90.10.deb

# Clean up
RUN rm -f elasticsearch-0.90.10.deb
RUN apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false
RUN rm -rf /var/lib/apt/lists/*

# Expose ports
EXPOSE 9200
EXPOSE 9300

# Define mountable directories.
VOLUME ["/usr/share/elasticsearch/data/"]

CMD /usr/share/elasticsearch/bin/elasticsearch -f
