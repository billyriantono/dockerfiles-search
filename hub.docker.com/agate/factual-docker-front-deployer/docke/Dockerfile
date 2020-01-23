# Gitit : Un wiki basé sur des fichiers Markdown et Git
#
# VERSION               140215
#

FROM     debian:wheezy
MAINTAINER Nico Dewaele "nico@adminrezo.fr"

ENV DEBIAN_FRONTEND noninteractive


# Depots, mises a jour et installs

RUN echo "deb http://ftp.fr.debian.org/debian/ wheezy main non-free contrib" > /etc/apt/sources.list
RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get install -y -q vim.tiny gitit ssh supervisor
RUN apt-get -y -q clean

RUN useradd wiki --shell=/bin/bash
RUN echo wiki:wiki | chpasswd
RUN mkdir /home/wiki
RUN chown wiki /home/wiki
RUN mkdir -p /var/run/sshd

ADD supervisor-gitit.conf /etc/supervisor/conf.d/supervisor-gitit.conf
EXPOSE 5001 22
CMD supervisord -n
