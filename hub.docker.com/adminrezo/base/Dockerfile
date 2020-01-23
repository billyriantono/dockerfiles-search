## TITLE : Base image for my Dockerfiles
### DESCRIPTION : Based on Debian Jessie (last update : 20-08-2015)

#! Usage :
#! `docker run -it adminrezo/base`

FROM		debian:jessie

MAINTAINER 	Nico Dewaele "nico@adminrezo.fr"

ENV DEBIAN_FRONTEND noninteractive

# Repos, upgrades, installs

RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get update && apt-get install -y -q vim.tiny git wget unzip
