FROM ubuntu:trusty
MAINTAINER Clark Laughlin <clark at laughlins dot org>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade
RUN apt-get install --no-install-recommends -y ssmtp vim mailutils
RUN apt-get install --no-install-recommends -y mono-complete
RUN apt-get clean
