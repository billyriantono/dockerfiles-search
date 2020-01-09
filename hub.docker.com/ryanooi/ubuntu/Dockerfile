FROM ubuntu:16.04

MAINTAINER ryan.ooi ryan.ooi@biwub.com

RUN apt-get update

RUN apt-get install -y \
    nginx \
    curl

# Add user tester and grant sudo permission
RUN useradd -m tester && adduser tester sudo
