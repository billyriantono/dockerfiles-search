FROM ubuntu:18.04
LABEL maintainer="administrator@unswpress.com"
LABEL description="Base UNSW Press Ubuntu dockerfile"
ENV UPDATED_AT 2018-08-28-1
ENV LANG en_AU.UTF-8
ENV LANGUAGE en_AU:en
ENV LC_ALL en_AU.UTF-8
RUN apt-get -qy update \
	&& apt-get -qy full-upgrade

# Internationalisation
RUN apt-get -qy install tzdata locales
RUN locale-gen en_AU.UTF-8 en_US.UTF-8 \
	&& update-locale LANG=$LANG LANGUAGE=$LANGUAGE LC_ALL=$LC_ALL

# Allow installing PPAs
RUN apt-get install -qy software-properties-common
RUN apt-get clean

