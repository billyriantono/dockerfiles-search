FROM ubuntu:bionic
LABEL maintainer="alexandre.allouche@xcg-consulting.fr"

# Define some ENV variables
# this will be used as the default backend option for confd
ENV CONFD_BACKEND env

# use existing locale
ENV LANG C.UTF-8

# add some system packages
RUN apt-get update && apt-get -y -q install \
	sudo less \
	net-tools \
	etcd-client \
	--no-install-recommends

# get latest stable confd
# ADD will always add downloaded files with a 600 permission
ADD https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd
