FROM phusion/baseimage:master
ENV DEBIAN_FRONTEND=noninteractive

#add this for mustache templates in config files
ADD https://raw.githubusercontent.com/tests-always-included/mo/master/mo /usr/bin/
RUN chmod a+x /usr/bin/mo

RUN apt-get update && \
    apt-get install gosu && \
    apt-get -y upgrade && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN add-apt-repository ppa:openjdk-r/ppa && \
    apt-get update  && \
    update-ca-certificates -f

RUN apt-get install -y openjdk-8-jre-headless && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
