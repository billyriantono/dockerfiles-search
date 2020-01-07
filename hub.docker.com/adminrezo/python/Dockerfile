## TITLE : Python image for Docker
### DESCRIPTION : Python 2 & 3 with iPython2 & 3

#! Usage :
#! It could not be more simple :
#! `docker run -it adminrezo/python bash`
#! or for Python stuffs
#! `docker run -it adminrezo/python python`
#! `docker run -it adminrezo/python ipython`
#! `docker run -it adminrezo/python python3`
#! `docker run -it adminrezo/python ipython3`


FROM     adminrezo/base
MAINTAINER Nico Dewaele "nico@adminrezo.fr"

ENV DEBIAN_FRONTEND noninteractive

RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get update && apt-get install -y -q ipython ipython3 python-pip python3-pip python-dev python3-dev
