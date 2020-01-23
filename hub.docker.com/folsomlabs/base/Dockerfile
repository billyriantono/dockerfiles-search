FROM ubuntu:14.04
MAINTAINER ben@folsomlabs.com

ENV DEBIAN_FRONTEND noninteractive

# Add our apt source
RUN echo "deb http://folsom-labs-artifacts.s3.amazonaws.com/apt trusty main" > /etc/apt/sources.list.d/folsomlabs.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 21E1FA28
RUN apt-get update

# Add our CA cert to the system
ADD folsomlabs_ca.crt /usr/local/share/ca-certificates/folsomlabs_ca.crt
RUN apt-get -qfy install ca-certificates
RUN /usr/sbin/update-ca-certificates

# Set default locale
RUN apt-get -qfy install locales
RUN locale-gen en_US.UTF-8; echo 'LANG="en_US.UTF-8"' > /etc/default/locale
RUN dpkg-reconfigure locales
ENV LANG en_US.UTF-8

# Essentials
RUN apt-get -qfy install jq curl wget
