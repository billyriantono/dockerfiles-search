FROM ubuntu:18.04 
MAINTAINER nandor "nandor@ntsj.com"

ADD startvm /

# install virtualbox 5.0
RUN apt-get update && \
    apt-get install -y virtualbox && \ 
    apt-get install -y virtualbox-dkms

# clean up
RUN apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* 

