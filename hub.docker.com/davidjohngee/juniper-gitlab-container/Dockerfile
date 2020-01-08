FROM ubuntu:16.04
MAINTAINER David Gee <david.gee@aronistgopher.com>
##########################################################
RUN apt-get update && apt-get install -y python-dev  \ 
			libxml2-dev python-pip libxslt1-dev build-essential  \ 
			libssl-dev libffi-dev git vim iputils-ping jq
RUN pip install cryptography junos-eznc jxmlease wget ansible==2.4.2.0 jsnapy requests ipaddress pyang pyangbind
RUN ansible-galaxy install Juniper.junos
RUN pip install python-heatclient
RUN pip install yamllint
WORKDIR /project
