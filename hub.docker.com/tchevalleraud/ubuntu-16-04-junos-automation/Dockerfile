FROM ubuntu:16.04
MAINTAINER Thibault CHEVALLERAUD <tchevalleraud@interdata.fr>
##########################################################
RUN apt-get update && apt-get install -y python-dev  \ 
			libxml2-dev python-pip libxslt1-dev build-essential  \ 
			libssl-dev libffi-dev git
RUN pip install cryptography junos-eznc jxmlease wget jsnapy requests ipaddress pyang pyangbind
WORKDIR /project