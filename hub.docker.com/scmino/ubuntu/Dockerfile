## See Description LABEL at the bottom ##

FROM             ubuntu:14.04
MAINTAINER       Sean Boran <sean_at_boran.com>

ENV REFRESHED_AT=2015-09-23 \
    DEBIAN_FRONTEND=noninteractive

RUN apt-get -qqy update && \
    apt-get -qqy upgrade 
    #dpkg-divert --local --rename --add /sbin/initctl && \
    #ln -sf /bin/true /sbin/initctl  

# Additional base packages
RUN \
  #apt-get -qy install apt-transport-https && \
  #apt-get -qy install language-pack-en && \
  apt-get -qy install openssh-server apt-file vim vim-tiny curl wget 
# software-properties-common
# gdebi-core puppet iperf traceroute git htop unzip 

RUN \
  apt-get -q autoclean

# space space form locales later
# apt-get install localepurge
#RUN /usr/sbin/locale-gen en_US 
#&& \
#/usr/sbin/update-locale LANG=en_US.UTF-8 LC_CTYPE=en_US.UTF-8

# ENV variables
# (note: ENV is one long line to minimise layers)
ENV \
  # Use a proxy for downloads?
  #ENV PROXY http://proxy.example.ch:80

  # Make sure we have a proper working terminal
  TERM=xterm 
# /ENV


#ADD ./start.sh /start.sh
#RUN chmod 755 /start.sh
#CMD ["/bin/bash", "/start.sh"]

LABEL Description="Base Ubuntu 14.04 tools added: git" Version="0.1"

# Dockerfile todo:
# - "DEBIAN_FRONTEND noninteractive" should be prefixed on each line to avoid a default

