FROM thstangenberg/baseimage

MAINTAINER Thorben Stangenberg <thorben@stangenberg.ch>

# update apt
RUN apt-get update

# install mysql client
RUN apt-get install -y mysql-client

# housekeeping
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*