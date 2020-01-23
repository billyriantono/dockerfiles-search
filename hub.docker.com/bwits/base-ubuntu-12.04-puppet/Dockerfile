FROM ubuntu:12.04
MAINTAINER Bill W
RUN apt-get -y install wget
RUN wget --no-check-certificate https://apt.puppetlabs.com/puppetlabs-release-precise.deb
RUN dpkg -i puppetlabs-release-precise.deb
RUN apt-get update
RUN apt-get -y install puppet facter
RUN puppet resource package puppet ensure=latest
RUN puppet resource package facter ensure=latest
RUN puppet resource package hiera  ensure=latest
