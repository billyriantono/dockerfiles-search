# ubuntu flask env
FROM ubuntu:14.04
MAINTAINER Joshua <joshua7v@hotmail.com>

# Update stuff
RUN apt-get update

# Install Python Setuptools
RUN apt-get --no-install-recommends install -y python python-setuptools libmysqld-dev libmysqlclient-dev build-essential python-dev

# Install pip
RUN easy_install pip

# Install flask
RUN pip install flask

EXPOSE 5000
