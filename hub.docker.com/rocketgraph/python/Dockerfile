#
# Rocketgraph Python
#

# Pull base image.
FROM rocketgraph/base-ubuntu

MAINTAINER Konstantinos Christofilos <kostas.christofilos@rocketgraph.com>

#Install Python
RUN apt-get -y update
RUN apt-get -y install python python-pip python-dev

VOLUME ["/python_app"]

WORKDIR "/python_app"