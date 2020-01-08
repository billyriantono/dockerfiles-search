FROM ubuntu:14.04

MAINTAINER RC

# ----------- Commands -------------
# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y vim nano wget supervisor unzip openssh-server && \
  mkdir -p /srv/var /var/log/supervisor /opt

# ----------- Configure SSH -------------
#RUN echo deb http://archive.ubuntu.com/ubuntu trusty main universe > /etc/apt/sources.list.d/trusty.list

# Clean
ADD es_docker_key.pub es_docker_key.pub

RUN \
  mkdir ~/.ssh && \
  touch ~/.ssh/authorized_keys && \
  cat es_docker_key.pub >> ~/.ssh/authorized_keys && \
  rm es_docker_key.pub && \
  /etc/init.d/ssh restart

# Start
EXPOSE 22
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"]