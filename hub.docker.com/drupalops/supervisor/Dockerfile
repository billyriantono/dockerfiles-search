FROM ubuntu:12.04

MAINTAINER Steve Oliver "https://github.com/steveoliver"

ENV DEBIAN_FRONTEND noninteractive

# make sure the package repository is up to date and update ubuntu
RUN apt-get update
RUN apt-get -y install python-software-properties
RUN add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) universe"
RUN apt-get update && apt-get -y upgrade
RUN locale-gen en_US.UTF-8
RUN apt-get -y install curl git man python-setuptools unzip vim wget

ENV LANG en_US.UTF-8
ENV LANGUAGE us_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV HOME /root

# supervisor installation &&
# create directory for child images to store configuration in.
RUN easy_install supervisor && \
  mkdir -p /var/log/supervisor && \
  mkdir -p /etc/supervisor/conf.d

# supervisor base configuration
ADD supervisord.conf /etc/supervisord.conf

# default command
CMD ["supervisord", "-n", "-c", "/etc/supervisord.conf"]
